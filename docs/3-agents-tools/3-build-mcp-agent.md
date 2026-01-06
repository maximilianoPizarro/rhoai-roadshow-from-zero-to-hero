# 🔧 Build MCP Agent

Now let's build the MCP Agent that will handle credit risk queries and updates for Neuralbank.

## MCP Agent Structure

The MCP Agent consists of:

1. **MCP Server**: Implements the Model Context Protocol
2. **Credit Risk Tools**: Functions to query and update credit risk
3. **Integration Layer**: Connects to Neuralbank's backend services
4. **Authentication**: Integrates with Keycloak

## Core Components

### 1. MCP Server Implementation

The MCP server exposes tools that can be called by AI assistants:

```java
package com.neuralbank.mcp;

import com.neuralbank.mcp.tools.CreditRiskTool;
import io.mcp.server.MCPServer;
import io.mcp.server.ToolRegistry;

public class NeuralbankMCPServer {
    
    private MCPServer server;
    private CreditRiskService creditRiskService;
    
    public void initialize() {
        server = new MCPServer.Builder()
            .withName("neuralbank-credit-risk")
            .withVersion("1.0.0")
            .build();
            
        // Register tools
        registerTools();
    }
    
    private void registerTools() {
        ToolRegistry registry = server.getToolRegistry();
        
        // Tool to query credit risk
        registry.register(new CreditRiskTool.QueryTool(creditRiskService));
        
        // Tool to update credit risk
        registry.register(new CreditRiskTool.UpdateTool(creditRiskService));
    }
    
    public void start() {
        server.start();
    }
}
```

### 2. Credit Risk Tools

Tools that interact with the credit risk service:

```java
package com.neuralbank.mcp.tools;

public class CreditRiskTool {
    
    public static class QueryTool implements MCPTool {
        private CreditRiskService service;
        
        @Override
        public String getName() {
            return "query_credit_risk";
        }
        
        @Override
        public String getDescription() {
            return "Query the current credit risk level for a customer";
        }
        
        @Override
        public MCPResult execute(MCPRequest request) {
            String customerId = request.getParameter("customer_id");
            CreditRisk risk = service.getCreditRisk(customerId);
            
            return MCPResult.success()
                .withData("customer_id", customerId)
                .withData("risk_level", risk.getLevel())
                .withData("score", risk.getScore())
                .withData("last_updated", risk.getLastUpdated());
        }
    }
    
    public static class UpdateTool implements MCPTool {
        private CreditRiskService service;
        
        @Override
        public String getName() {
            return "update_credit_risk";
        }
        
        @Override
        public String getDescription() {
            return "Update the credit risk level for a customer based on loan request";
        }
        
        @Override
        public MCPResult execute(MCPRequest request) {
            String customerId = request.getParameter("customer_id");
            String loanAmount = request.getParameter("loan_amount");
            String loanPurpose = request.getParameter("loan_purpose");
            
            CreditRiskUpdate update = service.updateCreditRisk(
                customerId, 
                loanAmount, 
                loanPurpose
            );
            
            return MCPResult.success()
                .withData("customer_id", customerId)
                .withData("previous_risk", update.getPreviousRisk())
                .withData("new_risk", update.getNewRisk())
                .withData("updated_at", update.getTimestamp());
        }
    }
}
```

### 3. Service Integration

Integration with Neuralbank's backend via Connectivity Link:

```java
package com.neuralbank.mcp.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class CreditRiskService {
    
    @Autowired
    private ConnectivityLinkClient connectivityLink;
    
    @Autowired
    private KeycloakAuthService keycloak;
    
    public CreditRisk getCreditRisk(String customerId) {
        // Authenticate via Keycloak
        String token = keycloak.getAccessToken();
        
        // Call credit risk service via Connectivity Link
        return connectivityLink.get(
            "/credit-risk-service/api/v1/risk/" + customerId,
            CreditRisk.class,
            token
        );
    }
    
    public CreditRiskUpdate updateCreditRisk(
        String customerId, 
        String loanAmount, 
        String loanPurpose
    ) {
        String token = keycloak.getAccessToken();
        
        UpdateRequest request = new UpdateRequest(loanAmount, loanPurpose);
        
        return connectivityLink.post(
            "/credit-risk-service/api/v1/risk/" + customerId + "/update",
            request,
            CreditRiskUpdate.class,
            token
        );
    }
}
```

## Configuration

### MCP Configuration (`mcp-config.yaml`)

```yaml
server:
  name: neuralbank-credit-risk
  version: 1.0.0
  port: 8080

tools:
  - name: query_credit_risk
    description: Query customer credit risk
    parameters:
      - name: customer_id
        type: string
        required: true
  - name: update_credit_risk
    description: Update customer credit risk
    parameters:
      - name: customer_id
        type: string
        required: true
      - name: loan_amount
        type: string
        required: true
      - name: loan_purpose
        type: string
        required: true

integration:
  keycloak:
    url: ${KEYCLOAK_URL}
    realm: neuralbank
  connectivity:
    baseUrl: ${CONNECTIVITY_LINK_URL}
```

### Application Properties

```properties
# Keycloak Configuration
keycloak.url=${KEYCLOAK_URL:http://keycloak.keycloak.svc.cluster.local}
keycloak.realm=neuralbank
keycloak.client-id=mcp-agent

# Connectivity Link
connectivity.base-url=${CONNECTIVITY_LINK_URL:http://connectivity-link.connectivity.svc.cluster.local}

# Credit Risk Service
credit-risk.service.url=${CREDIT_RISK_SERVICE_URL:http://credit-risk-service.neuralbank.svc.cluster.local}

# OpenTelemetry
otel.service.name=neuralbank-mcp-agent
otel.exporter.otlp.endpoint=http://otel-collector.observability.svc.cluster.local:4317
```

## Building the Agent

In your DevSpaces workspace:

```bash
# Build the project
mvn clean install

# Run tests
mvn test

# Package for deployment
mvn package
```

## Deployment Configuration

### Kubernetes Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: neuralbank-mcp-agent
  namespace: neuralbank-mcp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: neuralbank-mcp-agent
  template:
    metadata:
      labels:
        app: neuralbank-mcp-agent
    spec:
      containers:
      - name: mcp-agent
        image: neuralbank/mcp-agent:latest
        ports:
        - containerPort: 8080
        env:
        - name: KEYCLOAK_URL
          valueFrom:
            configMapKeyRef:
              name: mcp-config
              key: keycloak-url
        - name: CONNECTIVITY_LINK_URL
          valueFrom:
            configMapKeyRef:
              name: mcp-config
              key: connectivity-url
```

## Next Steps

Now that you've built the MCP Agent, let's test it using **MCP Inspector** and **Cursor** to verify everything works correctly.

Click **Test with MCP Inspector** to continue.

