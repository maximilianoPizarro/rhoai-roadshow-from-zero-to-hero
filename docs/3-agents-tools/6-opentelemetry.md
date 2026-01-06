# 📊 OpenTelemetry Observability

Observability is crucial for understanding how your MCP Agent performs in production. **OpenTelemetry** provides distributed tracing, metrics, and logs to help you monitor the entire system.

## What is OpenTelemetry?

**OpenTelemetry** is an open-source observability framework that provides:

- **Distributed Tracing**: Track requests across multiple services
- **Metrics**: Collect performance and business metrics
- **Logs**: Structured logging with correlation IDs
- **Instrumentation**: Automatic and manual code instrumentation

For Neuralbank, OpenTelemetry helps you:

- **Track Requests**: See how requests flow from frontend → MCP Agent → Backend
- **Identify Bottlenecks**: Find slow operations
- **Debug Issues**: Trace errors across services
- **Monitor Performance**: Track response times and throughput
- **Ensure Compliance**: Audit trail of all operations

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│              Commercial Agent (Frontend)                │
│                    [Trace Start]                         │
└────────────────────┬────────────────────────────────────┘
                     │
                     │ HTTP Request (Trace ID: abc123)
                     ▼
┌─────────────────────────────────────────────────────────┐
│              MCP Agent (OpenShift)                       │
│         [Span: MCP Request Processing]                   │
│                     │                                    │
│                     │ Keycloak Auth (Span)               │
│                     │ Connectivity Link (Span)           │
└────────────────────┬────────────────────────────────────┘
                     │
                     │ Service Call (Trace ID: abc123)
                     ▼
┌─────────────────────────────────────────────────────────┐
│         Credit Risk Service (Backend)                    │
│            [Span: Risk Update]                           │
│                     │                                    │
│                     │ Database Query (Span)              │
└────────────────────┬────────────────────────────────────┘
                     │
                     │ Response (Trace ID: abc123)
                     ▼
┌─────────────────────────────────────────────────────────┐
│            OpenTelemetry Collector                       │
│         [Aggregates All Spans]                           │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│         Observability Backend (Jaeger/Tempo)            │
│         [Stores and Visualizes Traces]                   │
└─────────────────────────────────────────────────────────┘
```

## Instrumenting the MCP Agent

### 1. Add Dependencies

Add OpenTelemetry dependencies to your `pom.xml`:

```xml
<dependencies>
    <!-- OpenTelemetry API -->
    <dependency>
        <groupId>io.opentelemetry</groupId>
        <artifactId>opentelemetry-api</artifactId>
        <version>1.32.0</version>
    </dependency>
    
    <!-- OpenTelemetry SDK -->
    <dependency>
        <groupId>io.opentelemetry</groupId>
        <artifactId>opentelemetry-sdk</artifactId>
        <version>1.32.0</version>
    </dependency>
    
    <!-- OpenTelemetry Exporter -->
    <dependency>
        <groupId>io.opentelemetry</groupId>
        <artifactId>opentelemetry-exporter-otlp</artifactId>
        <version>1.32.0</version>
    </dependency>
    
    <!-- OpenTelemetry Instrumentation -->
    <dependency>
        <groupId>io.opentelemetry.instrumentation</groupId>
        <artifactId>opentelemetry-spring-boot-starter</artifactId>
        <version>2.1.0</version>
    </dependency>
</dependencies>
```

### 2. Configure OpenTelemetry

Add configuration to `application.properties`:

```properties
# OpenTelemetry Configuration
otel.service.name=neuralbank-mcp-agent
otel.service.version=1.0.0

# OTLP Exporter
otel.exporter.otlp.endpoint=http://otel-collector.observability.svc.cluster.local:4317
otel.exporter.otlp.protocol=grpc

# Tracing
otel.traces.exporter=otlp
otel.metrics.exporter=otlp
otel.logs.exporter=otlp

# Sampling
otel.traces.sampler=traceidratio
otel.traces.sampler.arg=1.0
```

### 3. Instrument Code

Add tracing to your MCP Agent:

```java
package com.neuralbank.mcp;

import io.opentelemetry.api.OpenTelemetry;
import io.opentelemetry.api.trace.Span;
import io.opentelemetry.api.trace.Tracer;
import io.opentelemetry.api.trace.StatusCode;
import io.opentelemetry.context.Scope;

@Service
public class CreditRiskTool {
    
    private final Tracer tracer;
    
    public CreditRiskTool(OpenTelemetry openTelemetry) {
        this.tracer = openTelemetry.getTracer("neuralbank-mcp-agent");
    }
    
    public MCPResult queryCreditRisk(String customerId) {
        Span span = tracer.spanBuilder("query_credit_risk")
            .setAttribute("customer.id", customerId)
            .startSpan();
            
        try (Scope scope = span.makeCurrent()) {
            // Add span attributes
            span.setAttribute("tool.name", "query_credit_risk");
            span.setAttribute("customer.id", customerId);
            
            // Execute the query
            CreditRisk risk = creditRiskService.getCreditRisk(customerId);
            
            // Add result attributes
            span.setAttribute("risk.level", risk.getLevel());
            span.setAttribute("risk.score", risk.getScore());
            
            return MCPResult.success()
                .withData("customer_id", customerId)
                .withData("risk_level", risk.getLevel())
                .withData("score", risk.getScore());
                
        } catch (Exception e) {
            span.setStatus(StatusCode.ERROR, e.getMessage());
            span.recordException(e);
            throw e;
        } finally {
            span.end();
        }
    }
    
    public MCPResult updateCreditRisk(
        String customerId, 
        String loanAmount, 
        String loanPurpose
    ) {
        Span span = tracer.spanBuilder("update_credit_risk")
            .setAttribute("customer.id", customerId)
            .setAttribute("loan.amount", loanAmount)
            .setAttribute("loan.purpose", loanPurpose)
            .startSpan();
            
        try (Scope scope = span.makeCurrent()) {
            span.setAttribute("tool.name", "update_credit_risk");
            
            // Execute the update
            CreditRiskUpdate update = creditRiskService.updateCreditRisk(
                customerId, 
                loanAmount, 
                loanPurpose
            );
            
            // Add update attributes
            span.setAttribute("risk.previous", update.getPreviousRisk());
            span.setAttribute("risk.new", update.getNewRisk());
            span.setAttribute("update.timestamp", update.getTimestamp().toString());
            
            // Add business event
            span.addEvent("credit_risk_updated", 
                Attributes.of(
                    AttributeKey.stringKey("customer.id"), customerId,
                    AttributeKey.stringKey("risk.change"), 
                        update.getPreviousRisk() + " -> " + update.getNewRisk()
                )
            );
            
            return MCPResult.success()
                .withData("customer_id", customerId)
                .withData("previous_risk", update.getPreviousRisk())
                .withData("new_risk", update.getNewRisk());
                
        } catch (Exception e) {
            span.setStatus(StatusCode.ERROR, e.getMessage());
            span.recordException(e);
            throw e;
        } finally {
            span.end();
        }
    }
}
```

## Deploying OpenTelemetry Collector

### 1. Install OpenTelemetry Operator

```bash
oc apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/latest/download/opentelemetry-operator.yaml
```

### 2. Create Collector Configuration

```yaml
apiVersion: opentelemetry.io/v1alpha1
kind: OpenTelemetryCollector
metadata:
  name: otel-collector
  namespace: observability
spec:
  config: |
    receivers:
      otlp:
        protocols:
          grpc:
            endpoint: 0.0.0.0:4317
          http:
            endpoint: 0.0.0.0:4318
    
    processors:
      batch:
      resource:
        attributes:
          - key: service.name
            value: neuralbank-mcp-agent
            action: upsert
    
    exporters:
      jaeger:
        endpoint: jaeger-collector.observability.svc.cluster.local:14250
        tls:
          insecure: true
      logging:
        loglevel: debug
    
    service:
      pipelines:
        traces:
          receivers: [otlp]
          processors: [batch, resource]
          exporters: [jaeger, logging]
```

### 3. Deploy Jaeger (Observability Backend)

```bash
oc apply -f - <<EOF
apiVersion: jaegertracing.io/v1
kind: Jaeger
metadata:
  name: jaeger
  namespace: observability
spec:
  strategy: production
  storage:
    type: elasticsearch
    elasticsearch:
      nodeCount: 1
EOF
```

## Viewing Traces

### Access Jaeger UI

Navigate to Jaeger:
<a href="https://jaeger-query-observability.apps.<CLUSTER_DOMAIN>" target="_blank">https://jaeger-query-observability.apps.<CLUSTER_DOMAIN></a>

### Query Traces

1. **Select Service**: Choose `neuralbank-mcp-agent`
2. **Select Operation**: Choose `update_credit_risk` or `query_credit_risk`
3. **Set Time Range**: Select the time period
4. **Click "Find Traces"**

### Understanding Trace Views

**Trace Timeline**: See the complete request flow
- Frontend → MCP Agent → Credit Risk Service → Database
- See duration of each span
- Identify slow operations

**Span Details**: Click on any span to see:
- Attributes (customer ID, risk levels, etc.)
- Events (credit_risk_updated)
- Logs
- Tags

**Service Map**: Visualize service dependencies
- See how services connect
- Identify bottlenecks
- Monitor service health

## Example Trace

Here's what a complete trace looks like:

```
Trace: abc123def456
├─ Span: http_request (Frontend)
│  ├─ Duration: 2.5s
│  └─ Attributes:
│     ├─ http.method: POST
│     ├─ http.route: /mcp/tools/update_credit_risk
│     └─ customer.id: CUST-12345
│
├─ Span: mcp_request (MCP Agent)
│  ├─ Duration: 2.3s
│  ├─ Attributes:
│  │  ├─ tool.name: update_credit_risk
│  │  ├─ loan.amount: 50000
│  │  └─ loan.purpose: HOME_IMPROVEMENT
│  │
│  ├─ Span: keycloak_auth
│  │  └─ Duration: 0.1s
│  │
│  └─ Span: connectivity_link_call
│     ├─ Duration: 1.8s
│     └─ Attributes:
│        └─ service: credit-risk-service
│
└─ Span: credit_risk_update (Credit Risk Service)
   ├─ Duration: 1.5s
   ├─ Attributes:
   │  ├─ risk.previous: MEDIUM
   │  └─ risk.new: LOW
   │
   ├─ Event: credit_risk_updated
   │  └─ Timestamp: 2025-01-15T11:00:00Z
   │
   └─ Span: database_update
      └─ Duration: 0.3s
```

## Metrics and Dashboards

### Key Metrics to Monitor

- **Request Rate**: Requests per second
- **Error Rate**: Percentage of failed requests
- **Latency**: P50, P95, P99 response times
- **Tool Usage**: Which tools are used most
- **Customer Impact**: Number of credit risk updates

### Creating Dashboards

Use Grafana or OpenShift monitoring to create dashboards:

1. **MCP Agent Health**: Overall service health
2. **Tool Performance**: Performance by tool
3. **Error Analysis**: Error rates and types
4. **Business Metrics**: Credit risk updates per day

## Best Practices

✅ **Add Meaningful Attributes**: Include business context (customer ID, risk levels)  
✅ **Use Semantic Conventions**: Follow OpenTelemetry naming conventions  
✅ **Correlate Logs**: Use trace IDs in log messages  
✅ **Sample Appropriately**: Balance detail with performance  
✅ **Monitor Key Operations**: Focus on critical business operations  

## Compliance and Auditing

OpenTelemetry traces provide:

- **Complete Audit Trail**: Every operation is traced
- **Who**: User information from Keycloak
- **What**: Tool name and parameters
- **When**: Timestamps for all operations
- **Result**: Success or failure with details

This satisfies Neuralbank's compliance requirements for transparent and auditable operations.

## Next Steps

Congratulations! You've completed the full journey:

✅ Built and deployed an MCP Agent  
✅ Integrated with Neuralbank's systems  
✅ Set up comprehensive observability  

Your MCP Agent is now production-ready and helping Neuralbank accelerate credit decisions while maintaining compliance!

Return to the [main page](/) or explore the [Models section](../4-rhaiis/README.md) to learn about Red Hat AI Inference Server.

