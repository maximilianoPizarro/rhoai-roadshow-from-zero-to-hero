# 🤖 Deploy & Integrate

Now that your MCP Agent is built and tested, let's deploy it to OpenShift and integrate it with Neuralbank's frontend so commercial agents can use it.

## Deployment Strategy

We'll deploy the MCP Agent to OpenShift with:

- **High Availability**: Multiple replicas
- **Health Checks**: Liveness and readiness probes
- **Service Discovery**: Kubernetes services for internal communication
- **External Access**: Route for frontend integration
- **Monitoring**: OpenTelemetry instrumentation

## Deploying to OpenShift

### 1. Build Container Image

First, build and push your container image:

```bash
# Build the image
podman build -t neuralbank/mcp-agent:latest .

# Tag for OpenShift registry
podman tag neuralbank/mcp-agent:latest \
  image-registry.openshift-image-registry.svc:5000/neuralbank-mcp/mcp-agent:latest

# Push to registry
podman push image-registry.openshift-image-registry.svc:5000/neuralbank-mcp/mcp-agent:latest
```

Or use OpenShift BuildConfig:

```bash
oc new-build --name=mcp-agent \
  --strategy=docker \
  --dockerfile=- \
  --binary \
  -n neuralbank-mcp

oc start-build mcp-agent --from-dir=. --follow
```

### 2. Create Deployment

Apply the deployment configuration:

```bash
oc apply -f k8s/deployment.yaml -n neuralbank-mcp
```

### 3. Create Service

Expose the MCP Agent internally:

```bash
oc apply -f k8s/service.yaml -n neuralbank-mcp
```

### 4. Create Route

Expose the MCP Agent externally for frontend access:

```bash
oc expose svc neuralbank-mcp-agent \
  --name=neuralbank-mcp-agent \
  --port=8080 \
  -n neuralbank-mcp
```

Or create a Route with TLS:

```yaml
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: neuralbank-mcp-agent
  namespace: neuralbank-mcp
spec:
  to:
    kind: Service
    name: neuralbank-mcp-agent
  port:
    targetPort: 8080
  tls:
    termination: edge
    insecureEdgeTerminationPolicy: Redirect
```

## Frontend Integration

The frontend (Playground) needs to connect to your MCP Agent. The commercial agent interface will use the MCP protocol to communicate.

### Frontend Configuration

Update the frontend configuration to point to your MCP Agent:

```javascript
// frontend/src/config/mcp.js
export const MCP_CONFIG = {
  serverUrl: 'https://neuralbank-mcp-agent-neuralbank-mcp.apps.<CLUSTER_DOMAIN>',
  protocol: 'mcp',
  tools: [
    'query_credit_risk',
    'update_credit_risk'
  ]
};
```

### Chat Interface Integration

The Playground chat interface connects to the MCP Agent:

```javascript
// Example frontend integration
import { MCPServer } from '@modelcontextprotocol/sdk';

const mcpServer = new MCPServer({
  url: MCP_CONFIG.serverUrl,
  protocol: MCP_CONFIG.protocol
});

// Query credit risk
async function queryCreditRisk(customerId) {
  const result = await mcpServer.callTool('query_credit_risk', {
    customer_id: customerId
  });
  return result;
}

// Update credit risk
async function updateCreditRisk(customerId, loanAmount, loanPurpose) {
  const result = await mcpServer.callTool('update_credit_risk', {
    customer_id: customerId,
    loan_amount: loanAmount,
    loan_purpose: loanPurpose
  });
  return result;
}
```

## Testing the Integration

### 1. Verify Deployment

Check that your MCP Agent is running:

```bash
# Check pods
oc get pods -n neuralbank-mcp

# Check service
oc get svc -n neuralbank-mcp

# Check route
oc get route -n neuralbank-mcp
```

### 2. Test from Frontend

1. **Open Playground**: Navigate to the commercial agent interface
2. **Login**: Authenticate via Keycloak
3. **Test Query**: 
   ```
   "What is the credit risk for customer CUST-12345?"
   ```
4. **Verify Response**: Should see credit risk information
5. **Test Update**:
   ```
   "Update credit risk for customer CUST-12345 with a $50,000 home improvement loan"
   ```
6. **Verify Update**: Should see updated risk level

### 3. Verify Risk Update

After the commercial agent updates the risk:

1. **Query Again**: Ask for the same customer's risk
2. **Confirm Change**: The risk level should reflect the update
3. **Check Audit Trail**: Verify the update is logged

## End-to-End Flow

Here's the complete flow:

```
1. Commercial Agent (Frontend)
   │
   │ "Update credit risk for CUST-12345"
   │
   ▼
2. Playground Chat Interface
   │
   │ MCP Protocol Request
   │
   ▼
3. MCP Agent (OpenShift)
   │
   │ Authenticate via Keycloak
   │ Call Credit Risk Service via Connectivity Link
   │
   ▼
4. Credit Risk Service (Backend)
   │
   │ Update Database
   │
   ▼
5. MCP Agent
   │
   │ Return Updated Risk
   │
   ▼
6. Playground Chat Interface
   │
   │ Display Result
   │
   ▼
7. Commercial Agent
   "Credit risk updated from MEDIUM to LOW"
```

## Monitoring Deployment

Monitor your deployment:

```bash
# Watch pods
oc get pods -n neuralbank-mcp -w

# Check logs
oc logs -f deployment/neuralbank-mcp-agent -n neuralbank-mcp

# Check events
oc get events -n neuralbank-mcp --sort-by='.lastTimestamp'
```

## Troubleshooting

### Common Issues

**Pod Not Starting**:
- Check resource limits
- Verify image pull secrets
- Review pod logs

**Service Not Accessible**:
- Verify service selector matches pod labels
- Check service port configuration
- Test connectivity from another pod

**Authentication Failures**:
- Verify Keycloak configuration
- Check token expiration
- Validate client credentials

**Connectivity Link Issues**:
- Verify Connectivity Link service is running
- Check network policies
- Validate service endpoints

## Next Steps

Excellent! Your MCP Agent is deployed and integrated. Now let's set up **OpenTelemetry** to monitor distributed traces and ensure everything is working correctly.

Click **OpenTelemetry Observability** to continue.

