# 🔍 Test with MCP Inspector

Before deploying to production, it's crucial to test your MCP Agent. **MCP Inspector** is a tool that helps you validate MCP server functionality, and **Cursor** can be used to interact with your agent.

## What is MCP Inspector?

**MCP Inspector** is a testing and debugging tool for MCP servers. It allows you to:

- **List Available Tools**: See all tools your MCP server exposes
- **Test Tool Calls**: Execute tools with different parameters
- **Validate Responses**: Ensure tools return correct data
- **Debug Issues**: Identify problems before deployment

## Setting Up MCP Inspector

### Installation

MCP Inspector can be accessed via:

1. **Web Interface**: Available in your OpenShift cluster
2. **CLI Tool**: Install locally for command-line testing
3. **VS Code Extension**: Use within your development environment

### Accessing MCP Inspector

Navigate to MCP Inspector in your cluster:
<a href="https://mcp-inspector-mcp-inspector.apps.<CLUSTER_DOMAIN>" target="_blank">https://mcp-inspector-mcp-inspector.apps.<CLUSTER_DOMAIN></a>

## Testing Your MCP Agent

### 1. Connect to Your MCP Server

In MCP Inspector:

1. **Add Server**: Click "Add MCP Server"
2. **Enter Details**:
   - **Name**: `neuralbank-credit-risk`
   - **URL**: `http://neuralbank-mcp-agent.neuralbank-mcp.svc.cluster.local:8080`
   - **Protocol**: `MCP`

3. **Connect**: Click "Connect"

### 2. List Available Tools

Once connected, MCP Inspector will show:

- **Tools**: All available tools
  - `query_credit_risk`
  - `update_credit_risk`
- **Resources**: Available data resources
- **Prompts**: Pre-configured prompts

### 3. Test Query Tool

Test the `query_credit_risk` tool:

1. **Select Tool**: Click on `query_credit_risk`
2. **Enter Parameters**:
   ```json
   {
     "customer_id": "CUST-12345"
   }
   ```
3. **Execute**: Click "Execute Tool"
4. **Review Response**:
   ```json
   {
     "customer_id": "CUST-12345",
     "risk_level": "MEDIUM",
     "score": 650,
     "last_updated": "2025-01-15T10:30:00Z"
   }
   ```

### 4. Test Update Tool

Test the `update_credit_risk` tool:

1. **Select Tool**: Click on `update_credit_risk`
2. **Enter Parameters**:
   ```json
   {
     "customer_id": "CUST-12345",
     "loan_amount": "50000",
     "loan_purpose": "HOME_IMPROVEMENT"
   }
   ```
3. **Execute**: Click "Execute Tool"
4. **Review Response**:
   ```json
   {
     "customer_id": "CUST-12345",
     "previous_risk": "MEDIUM",
     "new_risk": "LOW",
     "updated_at": "2025-01-15T11:00:00Z"
   }
   ```

## Using Cursor to Test

**Cursor** can also interact with your MCP Agent directly. This simulates how commercial agents will use the system.

### Connect Cursor to MCP Server

1. **Open Cursor**: In your DevSpaces workspace or locally
2. **Configure MCP**: Add your MCP server configuration
3. **Test Queries**: Ask Cursor to use your MCP tools

### Example Cursor Queries

**Query Credit Risk**:
```
"Use the MCP agent to query credit risk for customer CUST-12345"
```

Cursor will:
1. Identify the appropriate tool (`query_credit_risk`)
2. Call the MCP server with the customer ID
3. Return the credit risk information

**Update Credit Risk**:
```
"Update credit risk for customer CUST-12345 with a loan request of $50,000 for home improvement"
```

Cursor will:
1. Use the `update_credit_risk` tool
2. Pass all required parameters
3. Return the updated risk level

## What is MCP Inspector?

MCP Inspector is a comprehensive testing tool that provides:

- **Tool Discovery**: Automatically discovers all tools your server exposes
- **Parameter Validation**: Ensures required parameters are provided
- **Response Validation**: Verifies responses match expected schemas
- **Error Handling**: Tests error scenarios and edge cases
- **Performance Metrics**: Measures response times and throughput

## Testing Scenarios

### Happy Path Tests

✅ **Query Existing Customer**: Should return valid risk data  
✅ **Update Risk Successfully**: Should update and return new risk level  
✅ **Multiple Concurrent Requests**: Should handle load  

### Error Handling Tests

❌ **Invalid Customer ID**: Should return appropriate error  
❌ **Missing Parameters**: Should validate and reject  
❌ **Service Unavailable**: Should handle backend failures gracefully  

### Integration Tests

🔗 **Keycloak Authentication**: Verify token handling  
🔗 **Connectivity Link**: Test service-to-service communication  
🔗 **Database Updates**: Confirm data persistence  

## Validation Checklist

Before moving to deployment, verify:

- [ ] All tools are discoverable
- [ ] Tools execute successfully with valid parameters
- [ ] Error handling works for invalid inputs
- [ ] Authentication via Keycloak functions correctly
- [ ] Connectivity Link integration works
- [ ] Responses match expected schemas
- [ ] Performance meets requirements (< 2s response time)

## Next Steps

Great! Your MCP Agent is tested and validated. Now let's **deploy it to OpenShift** and **integrate it with the frontend** so commercial agents can use it.

Click **Deploy & Integrate** to continue.

