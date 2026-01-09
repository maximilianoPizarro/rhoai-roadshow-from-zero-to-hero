# 💻 Working with DevSpaces

## What is DevSpaces?

**Red Hat DevSpaces** (formerly CodeReady Workspaces) provides cloud-based development environments that run directly on your OpenShift cluster. This means:

- **No Local Setup**: Everything runs in the cloud
- **Consistent Environment**: Same setup for all developers
- **Resource Efficiency**: Share cluster resources
- **Easy Collaboration**: Share workspaces with team members

For Kevin, DevSpaces means you can:
- Develop directly on OpenShift
- Access all cluster resources
- Test against real services
- Work with the generated `customer-service-mcp` code

## Accessing Your DevSpaces Workspace

The Golden Path template automatically creates a DevSpaces workspace configuration. Here's how to access it:

### Step 1: Navigate to DevSpaces

1. **From OpenShift Console**: Go to **Applications** → **Red Hat DevSpaces**
2. **Or access directly**: <a href="https://devspaces-<CLUSTER_DOMAIN>" target="_blank">https://devspaces-<CLUSTER_DOMAIN></a>

### Step 2: Open Your Workspace

1. **Find Your Workspace**: Look for a workspace named `customer-service-mcp`
2. **Click to Open**: This will launch your development environment

### Step 3: Wait for Startup

The workspace will automatically:
- Clone the generated repository
- Start all required containers
- Configure the development environment
- Install necessary tools and dependencies

## Workspace Features

Your DevSpaces workspace includes:

### Integrated Terminal
- Access to OpenShift CLI (`oc`)
- Direct access to cluster resources
- Run build and test commands
- Git operations

### Code Editor
- Full IDE experience in the browser
- IntelliSense and code completion
- Git integration
- Extension support
- Multi-file editing

### Port Forwarding
- Access services running in the cluster
- Test MCP Agent endpoints locally
- Connect to databases
- Debug running applications

### Volume Mounts
- Persistent storage for your code
- Shared volumes between containers
- ConfigMap and Secret mounts
- Workspace data persistence

## Development Workflow

In your DevSpaces workspace:

1. **Navigate to Code**: The generated `customer-service-mcp` code is already cloned
2. **Review Structure**: Explore the generated code structure
3. **Uncomment Code**: Find and uncomment the relevant sections (as mentioned in the template)
4. **Build**: Run `mvn clean install` to build the project
5. **Test**: Execute unit and integration tests
6. **Run Locally**: Use Quarkus dev mode for local testing
7. **Commit Changes**: Commit your uncommented code to start working

## Working with the Generated Code

The template generates code with commented sections. Your tasks:

1. **Uncomment Tools**: Find `QueryCreditRiskTool.java` and `UpdateCreditRiskTool.java`
2. **Review Implementation**: Understand how the tools work
3. **Configure Properties**: Update `application.properties` with your settings
4. **Test Locally**: Use Quarkus dev mode to test
5. **Commit**: Once ready, commit to enable Cursor and Playground integration

## Connecting to Cluster Services

From your DevSpaces workspace, you can:

- **Access Keycloak**: Test authentication flows
- **Connect to Credit Risk Service**: Test integration via Connectivity Link
- **Use Connectivity Link**: Verify service-to-service communication
- **Access OpenTelemetry**: View traces and metrics
- **View Topology**: Access OpenShift topology view to see the architecture

## Viewing the Neuralbank Topology

To observe the complete Neuralbank architecture:

1. **OpenShift Console**: Navigate to your project (`neuralbank` - Neuralbank project)
2. **Topology View**: Click on "Topology" in the left menu
3. **View Architecture**: You'll see all services including:
   - Frontend services
   - Keycloak
   - Connectivity Link components
   - Backend services
   - Your `customer-service-mcp` (once deployed)

?> **Note** You may need to authenticate in the OpenShift console to view the topology. Use your provided credentials.

## Next Steps

Now that your DevSpaces workspace is ready, let's start **building and configuring the MCP Agent** (`customer-service-mcp`) that will query and update credit risk information.

Click **Build MCP Agent** to continue.
