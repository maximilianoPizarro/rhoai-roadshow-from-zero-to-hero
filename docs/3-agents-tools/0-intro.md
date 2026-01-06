# 🎯 Introduction to MCP Agents

## What is MCP?

**Model Context Protocol (MCP)** is an open protocol that enables AI assistants to securely access external data sources and tools. MCP servers provide a standardized way for AI applications to interact with various services, databases, and APIs.

For Neuralbank, MCP Agents serve as intelligent intermediaries that:

- **Query Credit Risk Data**: Retrieve customer credit risk information from backend services
- **Update Risk Levels**: Modify credit risk assessments based on loan requests
- **Provide Transparency**: Maintain audit trails for compliance
- **Accelerate Decisions**: Automate manual processes to speed up loan approvals

## The Neuralbank MCP Agent

The MCP Agent you'll build will:

1. **Receive Queries**: Commercial agents query customer credit risk via chat interface
2. **Process Requests**: The MCP Agent processes the query and determines required actions
3. **Interact with Services**: Connects to Neuralbank's credit risk service via Connectivity Link
4. **Update Risk Levels**: Modifies credit risk based on loan request parameters
5. **Return Results**: Provides updated information back to the commercial agent

## Architecture Flow

```
Commercial Agent (Frontend)
         │
         │ Chat Query: "Update credit risk for customer X"
         ▼
    MCP Agent (OpenShift)
         │
         │ Query Credit Risk Service
         ▼
    Credit Risk Service (Backend)
         │
         │ Update Risk Level
         ▼
    Database
         │
         │ Return Updated Risk
         ▼
    MCP Agent
         │
         │ Return Result
         ▼
Commercial Agent (Frontend)
    "Credit risk updated successfully"
```

## Key Components

### MCP Server
The MCP server runs on OpenShift and implements the Model Context Protocol. It exposes:
- **Tools**: Functions that can query and update credit risk
- **Resources**: Access to credit risk data
- **Prompts**: Pre-configured prompts for common operations

### Integration Points
- **Keycloak**: Authentication and authorization
- **Connectivity Link**: Service-to-service communication
- **Credit Risk Service**: Backend Java service managing risk data
- **Frontend**: Commercial agent chat interface (Playground)

## Benefits for Neuralbank

✅ **Faster Decisions**: Reduce credit approval time from days to minutes  
✅ **Scalability**: Handle increasing loan volumes without proportional staff increases  
✅ **Compliance**: Full audit trail of all operations  
✅ **Transparency**: Clear visibility into risk assessment changes  
✅ **Developer Experience**: Easy to develop, test, and deploy using Golden Path  

## What's Next?

Now that you understand the basics, let's explore the **Golden Path** that the Platform Engineering team has prepared for you. This will make it easy to get started with your development environment.

Click **Golden Path & Developer Hub** to continue.
