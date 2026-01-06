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

3. Search for templates related to:
   - **MCP Agents**
   - **Java Services**
   - **OpenShift AI**

## Using Cursor with Developer Hub

**Cursor** is an AI-powered code editor that can interact with Developer Hub to help you find and use Software Templates.

### Finding the Right Template

As Kevin, you need to find a Software Template that supports:
- MCP Agent development
- Java backend integration
- OpenShift deployment
- DevSpaces workspace generation

### Steps to Find Your Template

1. **Open Cursor** in your development environment

2. **Query Developer Hub**: Ask Cursor:
   ```
   "Search Developer Hub for MCP Agent templates with Java support"
   ```

3. **Review Templates**: Cursor will show you available templates that match your needs

4. **Select Template**: Choose the template that best fits the Neuralbank MCP Agent requirements

### The Neuralbank MCP Template

The Platform Engineering team has created a specific template for Neuralbank MCP Agents that includes:

- ✅ MCP server skeleton code
- ✅ Java service integration examples
- ✅ Keycloak authentication setup
- ✅ Connectivity Link configuration
- ✅ OpenTelemetry instrumentation
- ✅ DevSpaces workspace configuration
- ✅ Testing framework setup
- ✅ CI/CD pipeline templates

## Generating Your Project

Once you've found the right template:

1. **Fill in Parameters**:
   - Project name: `neuralbank-mcp-agent`
   - Namespace: `neuralbank-mcp`
   - Git repository: Your repository URL

2. **Generate Project**: Click "Generate" or use Cursor to trigger generation

3. **Review Generated Code**: The template creates:
   - Source code structure
   - Configuration files
   - CI/CD pipelines
   - Documentation
   - Test suites

## What Gets Generated

The Golden Path template generates:

```
neuralbank-mcp-agent/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/neuralbank/mcp/
│   │   │       ├── CreditRiskAgent.java
│   │   │       ├── MCPServer.java
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
├── pom.xml (or build.gradle)
├── README.md
└── .gitignore
```

## Next Steps

Now that you understand the Golden Path and Developer Hub, let's set up your **DevSpaces workspace** to start developing directly on OpenShift.

Click **DevSpaces Workspace** to continue.

