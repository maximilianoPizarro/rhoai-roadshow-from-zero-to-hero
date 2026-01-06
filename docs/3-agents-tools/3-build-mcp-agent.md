# 🔧 Build MCP Agent (customer-service-mcp)

Now let's work with the `customer-service-mcp` service that was generated from the Golden Path template. This Quarkus-based MCP server handles credit risk queries and updates for Neuralbank.

## Service Overview

The `customer-service-mcp` service is a **Quarkus MCP Server** that:

1. **Implements MCP Protocol**: Provides standardized interface for AI assistants
2. **Exposes Credit Risk Tools**: Functions to query and update credit risk
3. **Integrates with Backend**: Connects to Neuralbank's services via Connectivity Link
4. **Handles Authentication**: Uses Keycloak for secure access

![Customer Service MCP Component](../images/customer-service-mcp-component.png)

## Generated Code Structure

The Golden Path template generated a complete Quarkus project with:

```
customer-service-mcp/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/neuralbank/mcp/
│   │   │       ├── CustomerServiceMCPServer.java  (Main server class)
│   │   │       ├── tools/
│   │   │       │   ├── QueryCreditRiskTool.java   (Commented - needs uncommenting)
│   │   │       │   └── UpdateCreditRiskTool.java  (Commented - needs uncommenting)
│   │   │       └── service/
│   │   │           └── CreditRiskService.java     (Integration layer)
│   │   └── resources/
│   │       ├── application.properties             (Configuration)
│   │       └── mcp-config.yaml                    (MCP configuration)
│   └── test/
├── .devcontainer/
│   └── devcontainer.json                          (DevSpaces config)
├── pom.xml                                         (Maven dependencies)
└── README.md
```

## Kevin's First Task: Uncomment the Code

The template generates code with **intentional commented sections**. This allows you to:

1. **Understand the Structure**: See how everything fits together
2. **Learn by Doing**: Uncomment and configure step by step
3. **Customize**: Adapt the code to your specific needs

### Step 1: Open the Project in DevSpaces

1. **Navigate to DevSpaces**: Open your workspace
2. **Open Project**: Navigate to the `customer-service-mcp` directory
3. **Explore Structure**: Review the generated code

### Step 2: Uncomment QueryCreditRiskTool

1. **Open File**: `src/main/java/com/neuralbank/mcp/tools/QueryCreditRiskTool.java`
2. **Find Commented Code**: Look for sections marked with `// TODO: Uncomment this section`
3. **Uncomment**: Remove the comment markers and review the implementation
4. **Understand**: Read through the code to understand how it queries credit risk

### Step 3: Uncomment UpdateCreditRiskTool

1. **Open File**: `src/main/java/com/neuralbank/mcp/tools/UpdateCreditRiskTool.java`
2. **Find Commented Code**: Look for the update implementation
3. **Uncomment**: Remove comment markers
4. **Review**: Understand how it updates credit risk levels

### Step 4: Review Configuration

1. **application.properties**: Check configuration values
   - Keycloak URL
   - Connectivity Link endpoints
   - Service URLs
   - OpenTelemetry settings

2. **mcp-config.yaml**: Review MCP server configuration
   - Tool definitions
   - Resource definitions
   - Prompt templates

### Step 5: Build and Test Locally

In your DevSpaces terminal:

```bash
# Navigate to project
cd customer-service-mcp

# Build the project
mvn clean install

# Run in dev mode (Quarkus)
mvn quarkus:dev
```

The service will start in development mode, allowing you to:
- Test endpoints locally
- See live code reloading
- Debug issues
- View logs

### Step 6: Commit Your Changes

Once you've uncommented the code and verified it builds:

```bash
# Stage changes
git add .

# Commit
git commit -m "Uncomment MCP tools implementation"

# Push (if repository is configured)
git push
```

?> **Important**: This commit enables the integration with Cursor and Playground. The service needs to be committed before it can be used in the LlamaStack Playground.

## Understanding the Code

### MCP Server Implementation

The main server class (`CustomerServiceMCPServer.java`) sets up the MCP protocol server:

- **Registers Tools**: Makes tools available to AI assistants
- **Handles Requests**: Processes MCP protocol messages
- **Manages Lifecycle**: Starts and stops the server

### Credit Risk Tools

The tools you uncommented provide:

1. **QueryCreditRiskTool**: 
   - Queries current credit risk for a customer
   - Returns risk level, score, and last update time

2. **UpdateCreditRiskTool**:
   - Updates credit risk based on loan request
   - Takes customer ID, loan amount, and purpose
   - Returns previous and new risk levels

### Integration Layer

The `CreditRiskService` handles:
- **Keycloak Authentication**: Gets access tokens
- **Connectivity Link**: Makes secure service-to-service calls
- **Error Handling**: Manages failures gracefully
- **OpenTelemetry**: Adds tracing spans

## Development Workflow

Since the service is developed in DevSpaces (not deployed with `oc` commands), your workflow is:

1. **Edit Code**: Make changes in DevSpaces editor
2. **Build Locally**: Use `mvn clean install`
3. **Test Locally**: Use `mvn quarkus:dev`
4. **Commit Changes**: Git commit and push
5. **Test in Playground**: Use LlamaStack Playground to test MCP integration

## Testing the Service

### Local Testing

With Quarkus dev mode running:

```bash
# Test health endpoint
curl http://localhost:8080/health

# Test MCP endpoint (if exposed)
curl http://localhost:8080/mcp/tools
```

### Integration Testing

Once committed, test in LlamaStack Playground:
1. **Open Playground**: Navigate to LlamaStack Playground
2. **Select MCP Server**: Choose `customer-service-mcp`
3. **Test Tools**: Try querying and updating credit risk

## Next Steps

Now that you've uncommented the code and committed it, let's test the service using **MCP Inspector** and **Cursor** to verify everything works correctly.

Click **Test with MCP Inspector** to continue.
