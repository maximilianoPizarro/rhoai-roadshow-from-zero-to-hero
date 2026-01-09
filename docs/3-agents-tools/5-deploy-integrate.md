# 🤖 Deploy & Integrate

Now that your `customer-service-mcp` is built and tested in DevSpaces, let's integrate it with LlamaStack Playground so commercial agents can use it.

## Development Approach

**Important**: The `customer-service-mcp` service is **not deployed using `oc` commands**. Instead:

- **Developed in DevSpaces**: All development happens in your DevSpaces workspace
- **Tested Locally**: Use Quarkus dev mode for local testing
- **Integrated via Git**: Committed code is automatically available to Playground
- **Runtime in OpenShift**: The service runs automatically when accessed via Playground

## Integration with LlamaStack Playground

The `customer-service-mcp` integrates with LlamaStack Playground, allowing commercial agents to interact with the credit risk system through a chat interface.

### Step 1: Verify Service is Committed

Ensure your uncommented code is committed:

```bash
# Check git status
git status

# If there are uncommitted changes, commit them
git add .
git commit -m "Uncomment and configure MCP tools"
git push
```

### Step 2: Access LlamaStack Playground

1. **Navigate to Playground**:
   <a href="https://llama-stack-playground-llama-stack.apps.<CLUSTER_DOMAIN>" target="_blank">https://llama-stack-playground-llama-stack.apps.<CLUSTER_DOMAIN></a>

2. **Login**: Authenticate via Keycloak (see [Keycloak User Management](2.5-keycloak-user-management.md))

![Neuralbank Home](../images/neuralbank-home.png)

### Step 3: Select MCP Server

1. **Open MCP Settings**: In Playground, navigate to MCP server configuration
2. **Select customer-service-mcp**: Choose your service from the list
3. **Verify Connection**: Ensure the service is connected and tools are available

![Customer Service](../images/customer-service.png)

### Step 4: Test Query Tool

Test the `query_credit_risk` tool:

1. **Open Chat**: Start a new chat session in Playground
2. **Query Credit Risk**: Type:
   ```
   "What is the credit risk for customer CUST-12345?"
   ```
3. **Review Response**: The MCP agent should return credit risk information

### Step 5: Test Update Tool

Test the `update_credit_risk` tool:

1. **Update Request**: Type:
   ```
   "Update credit risk for customer CUST-12345 with a $50,000 home improvement loan"
   ```
2. **Review Response**: Should show updated risk level

![Update Risk Level](../images/update-risk-level.png)

### Step 6: Verify Risk Update

After updating the risk:

1. **Query Again**: Ask for the same customer's risk
2. **Confirm Change**: The risk level should reflect the update
3. **Check Audit Trail**: Verify the update is logged in OpenTelemetry

## End-to-End Flow

Here's the complete flow:

```
1. Commercial Agent (Playground)
   │
   │ "Update credit risk for CUST-12345"
   │ (Authenticated via Keycloak)
   │
   ▼
2. LlamaStack Playground
   │
   │ MCP Protocol Request
   │
   ▼
3. customer-service-mcp (DevSpaces/OpenShift)
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
5. customer-service-mcp
   │
   │ Return Updated Risk via MCP
   │
   ▼
6. LlamaStack Playground
   │
   │ Display Result
   │
   ▼
7. Commercial Agent
   "Credit risk updated from MEDIUM to LOW"
```

## Testing from Playground

### Using Cursor in Playground

You can also use Cursor to interact with the MCP agent:

![Cursor Prompt](../images/cursor-prompt.png)

1. **Open Cursor**: In your DevSpaces workspace or locally
2. **Configure MCP**: Point Cursor to your `customer-service-mcp` service
3. **Test Queries**: Ask Cursor to use MCP tools

![Cursor Prompt 2](../images/cursor-prompt-2.png)

### Example Cursor Queries

**Query Credit Risk**:
```
"Use the customer-service-mcp to query credit risk for customer CUST-12345"
```

**Update Credit Risk**:
```
"Update credit risk for customer CUST-12345 with a $50,000 home improvement loan using customer-service-mcp"
```

## Monitoring Integration

### View in OpenShift Topology

1. **OpenShift Console**: Navigate to `neuralbank` project (Neuralbank project)
2. **Topology View**: See `customer-service-mcp` in the topology
3. **Service Connections**: View how it connects to other services

### View in OpenTelemetry

See [OpenTelemetry Observability](6-opentelemetry.md) for details on viewing traces and logs.

## Troubleshooting

### Service Not Available in Playground

- **Check Git Commit**: Ensure code is committed and pushed
- **Verify Service Running**: Check if service is running in DevSpaces
- **Check MCP Configuration**: Verify MCP server configuration

### Authentication Issues

- **Keycloak Login**: Ensure you're logged in via Keycloak
- **Token Validity**: Check if tokens are expired
- **User Permissions**: Verify user has required roles

### Connectivity Link Issues

- **Service Discovery**: Check if services are discoverable
- **Network Policies**: Verify network policies allow communication
- **Rate Limits**: Check if rate limits are being hit

## Next Steps

Excellent! Your `customer-service-mcp` is integrated with Playground. Now let's set up **OpenTelemetry** to monitor distributed traces and ensure everything is working correctly.

Click **OpenTelemetry Observability** to continue.
