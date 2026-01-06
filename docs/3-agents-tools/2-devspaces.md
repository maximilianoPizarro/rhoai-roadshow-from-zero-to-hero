# 💻 DevSpaces Workspace

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
- Deploy without context switching

## Creating Your DevSpaces Workspace

### From the Generated Template

If you used the Golden Path template, it includes a `.devcontainer/devcontainer.json` file that defines your DevSpaces workspace.

### Manual Setup

If you need to create a workspace manually:

1. **Navigate to DevSpaces**:
   - From OpenShift Console, go to **Applications** → **Red Hat DevSpaces**
   - Or access directly: <a href="https://devspaces-<CLUSTER_DOMAIN>" target="_blank">https://devspaces-<CLUSTER_DOMAIN></a>

2. **Create Workspace**:
   - Click **Create Workspace**
   - Select your project: `neuralbank-mcp`
   - Choose the Devfile from your repository (if available)

3. **Configure Workspace**:
   - **Name**: `neuralbank-mcp-dev`
   - **Source**: Your Git repository URL
   - **Devfile**: Use the devfile from the Golden Path template

## Devfile Configuration

The Devfile defines your development environment. Here's an example for the Neuralbank MCP Agent:

```yaml
schemaVersion: 2.2.0
metadata:
  name: neuralbank-mcp-agent
  version: 1.0.0
components:
  - name: java
    container:
      image: registry.redhat.io/devspaces/maven-rhel8:latest
      memoryLimit: 2Gi
      cpuLimit: 1
      env:
        - name: JAVA_HOME
          value: /usr/lib/jvm/java-11
  - name: mcp-server
    container:
      image: registry.redhat.io/ubi8/nodejs-18:latest
      memoryLimit: 1Gi
      command: ['sleep', 'infinity']
  - name: tools
    container:
      image: registry.redhat.io/ubi8/ubi:latest
      memoryLimit: 512Mi
      command: ['sleep', 'infinity']
commands:
  - id: build
    exec:
      component: java
      command: mvn clean install
  - id: test
    exec:
      component: java
      command: mvn test
  - id: run-mcp
    exec:
      component: mcp-server
      command: npm start
```

## Workspace Features

Your DevSpaces workspace includes:

### Integrated Terminal
- Access to OpenShift CLI (`oc`)
- Direct access to cluster resources
- Run build and test commands

### Code Editor
- Full IDE experience in the browser
- IntelliSense and code completion
- Git integration
- Extension support

### Port Forwarding
- Access services running in the cluster
- Test MCP Agent endpoints
- Connect to databases

### Volume Mounts
- Persistent storage for your code
- Shared volumes between containers
- ConfigMap and Secret mounts

## Accessing Your Workspace

1. **Open Workspace**: Click on your workspace name in DevSpaces

2. **Wait for Startup**: The workspace will start all defined containers

3. **Access Terminal**: Open a terminal to start working

4. **Clone Repository** (if not auto-cloned):
   ```bash
   git clone https://github.com/your-org/neuralbank-mcp-agent.git
   cd neuralbank-mcp-agent
   ```

## Development Workflow

In your DevSpaces workspace:

1. **Edit Code**: Use the integrated editor
2. **Build**: Run `mvn clean install` or your build command
3. **Test**: Execute unit and integration tests
4. **Debug**: Use breakpoints and debugger
5. **Deploy**: Use `oc` commands to deploy to OpenShift

## Connecting to Cluster Services

From your DevSpaces workspace, you can:

- **Access Keycloak**: Test authentication flows
- **Connect to Credit Risk Service**: Test integration
- **Use Connectivity Link**: Verify service-to-service communication
- **Access OpenTelemetry**: View traces and metrics

## Next Steps

Now that your DevSpaces workspace is ready, let's start **building the MCP Agent** that will query and update credit risk information.

Click **Build MCP Agent** to continue.

