# 🛤️ Golden Path & Developer Hub

## What is the Golden Path?

The **Golden Path** is a curated set of best practices, standards, and tools that the Platform Engineering team has established to improve Developer Experience. It provides:

- **Pre-configured Templates**: Software Templates with everything you need
- **Best Practices**: Industry-standard patterns and conventions
- **Quality Standards**: Built-in testing, security, and compliance checks
- **Quick Start**: Get productive in minutes, not days

For Kevin (and you), the Golden Path means you can:

1. Find a Software Template that matches your needs
2. Generate a complete development environment
3. Start coding immediately with all dependencies configured
4. Deploy with confidence knowing best practices are followed

## Developer Hub

**Red Hat Developer Hub** is a centralized portal where developers can discover and use Software Templates. It integrates with tools like **Cursor** to provide a seamless development experience.

### Accessing Developer Hub

1. Navigate to the Developer Hub:
   <a href="https://developer-hub-developer-hub.apps.<CLUSTER_DOMAIN>" target="_blank">https://developer-hub-developer-hub.apps.<CLUSTER_DOMAIN></a>

2. You'll see a catalog of available Software Templates

![Developer Hub](../images/developer-hub.png)

## Using the Golden Path Template

The Platform Engineering team has created a specific template for Neuralbank MCP Agents called **Quarkus MCP Server**. This template generates the `customer-service-mcp` service with:

- ✅ Quarkus MCP server skeleton code
- ✅ Java service integration examples
- ✅ Keycloak authentication setup
- ✅ Connectivity Link configuration
- ✅ OpenTelemetry instrumentation
- ✅ DevSpaces workspace configuration
- ✅ Testing framework setup
- ✅ CI/CD pipeline templates

### Step 1: Find the Template

1. **Open Developer Hub**: Navigate to Developer Hub in your browser

2. **Search for Template**: Look for "Quarkus MCP Server" or "customer-service-mcp"

![Quarkus MCP Template](../images/quarkus-mcp-template.png)

### Step 2: Create from Template

1. **Click on Template**: Select the "Quarkus MCP Server" template

2. **Fill in Parameters**:
   - **Application Name**: `customer-service-mcp`
   - **Project Name**: `neuralbank-mcp`
   - **Git Repository**: Your repository URL (or leave default)
   - **Namespace**: `neuralbank-mcp`

![Customer Service MCP Template](../images/customer-service-mcp-template.png)

3. **Review Configuration**: The template will show you what will be generated

![Customer Service MCP Template Review](../images/customer-service-mcp-template-review.png)

### Step 3: Generate the Project

1. **Click "Create"**: This will generate the project structure

2. **Wait for Generation**: The template will create:
   - Source code structure
   - Configuration files
   - CI/CD pipelines
   - Documentation
   - Test suites

![Customer Service MCP Template 2](../images/customer-service-mcp-template-2.png)

![Customer Service MCP Template 3](../images/customer-service-mcp-template-3.png)

### Step 4: Review Generated Code

The template generates a Quarkus-based MCP server with:

- **MCP Server Implementation**: Ready-to-use MCP protocol implementation
- **Credit Risk Tools**: Skeleton code for query and update operations
- **Integration Layer**: Connectivity Link and Keycloak integration
- **OpenTelemetry**: Pre-configured observability

![Quarkus MCP Server](../images/quarkus-mcp-server.png)

## What Gets Generated

The Golden Path template generates:

```
customer-service-mcp/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/neuralbank/mcp/
│   │   │       ├── CustomerServiceMCPServer.java
│   │   │       ├── tools/
│   │   │       │   ├── QueryCreditRiskTool.java
│   │   │       │   └── UpdateCreditRiskTool.java
│   │   │       └── ...
│   │   └── resources/
│   │       ├── application.properties
│   │       └── mcp-config.yaml
│   └── test/
├── .devcontainer/
│   └── devcontainer.json
├── .github/
│   └── workflows/
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
├── pom.xml
├── README.md
└── .gitignore
```

## Important: Code is Pre-configured

The generated code includes **commented-out sections** that Kevin needs to uncomment and configure. This is intentional - it allows you to:

1. Understand the code structure
2. Learn by doing
3. Configure for your specific needs

**Kevin's First Task**: After the template generates the code, you'll need to:
1. Uncomment the relevant code sections
2. Review and understand the implementation
3. Commit the changes to start working with Cursor and Playground

## Next Steps

Now that you understand the Golden Path and Developer Hub, let's set up your **DevSpaces workspace** to start developing directly on OpenShift.

Click **Working with DevSpaces** to continue.
