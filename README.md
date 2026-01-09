# IA Development From Zero To Hero

This repository contains the **IA Development From Zero To Hero** workshop - a comprehensive journey from business use case to production-ready AI solution using Model Context Protocol (MCP) Agents.

The complete documentation is available at: [https://maximilianoPizarro.github.io/rhoai-roadshow-from-zero-to-hero/](https://maximilianoPizarro.github.io/rhoai-roadshow-from-zero-to-hero/)

## 📖 About This Workshop

This workshop takes you through a complete journey from understanding a business use case to deploying a production-ready AI solution. You'll learn how to build MCP Agents that integrate with enterprise systems, providing intelligent automation while maintaining security, compliance, and observability.

## 🏦 Business Use Case: Neuralbank

**Neuralbank** is a financial institution that provides loans to customers. The challenge: customers experience significant delays in obtaining credit due to manual credit risk assessment processes. 

**The Solution**: Build an MCP Agent that allows commercial agents to query and update credit risk information through a chat interface, accelerating credit decisions while maintaining full compliance and auditability.

## 👨‍💻 Your Role: Kevin, Java Developer

You are **Kevin**, a new Java developer joining Neuralbank's development team. Your mission is to build an MCP Agent (`customer-service-mcp`) that integrates with Neuralbank's infrastructure to automate credit risk management.

### What You'll Build

- **MCP Agent**: A Quarkus-based service that implements the Model Context Protocol
- **Integration**: Connect with Neuralbank's credit risk service via Connectivity Link
- **Authentication**: Secure access using Keycloak
- **Chat Interface**: Enable commercial agents to interact via Playground (OpenShift AI)
- **Observability**: Full distributed tracing with OpenTelemetry

## 🛠️ Technologies & Tools

This workshop showcases:

- **Red Hat OpenShift AI**: Platform for AI/ML workloads
- **Model Context Protocol (MCP)**: Open protocol for AI assistants
- **LlamaStack**: Open-source framework for generative AI applications
- **Red Hat DevSpaces**: Cloud-based development environments
- **Red Hat Developer Hub**: Centralized portal with Software Templates
- **Quarkus**: Java framework for cloud-native microservices
- **Keycloak**: Authentication and authorization
- **Connectivity Link**: Service mesh for secure communication
- **OpenTelemetry**: Observability framework
- **GitLab**: Source code management and CI/CD
- **ArgoCD**: GitOps for declarative deployments

## 🎯 Learning Path

### 1. Getting Connected
- Understand the Neuralbank business case
- Configure your environment
- Verify access to platform services (OpenShift Console, SSO, GitLab, Quay, Developer Hub)

### 2. MCP Agents & Tools
- **Golden Path**: Use Developer Hub Software Templates to generate the MCP service
- **DevSpaces**: Develop in cloud-based workspaces
- **Build MCP Agent**: Uncomment and configure pre-generated code
- **Keycloak User Management**: Create and manage users
- **Connectivity Link**: Understand service mesh communication
- **MCP Inspector**: Test and validate your agent
- **Deploy & Integrate**: Connect with Playground
- **OpenTelemetry**: Monitor distributed traces

### 3. Resources
- Source code repositories
- Installation methods (Ansible, Helm, GitOps)
- Additional documentation

## 🚀 Quick Start

1. **Access the Documentation**: Visit [https://maximilianoPizarro.github.io/rhoai-roadshow-from-zero-to-hero/](https://maximilianoPizarro.github.io/rhoai-roadshow-from-zero-to-hero/)

2. **Set Your Cluster Domain**: Use the navigation bar at the top to set your cluster domain and click `Save`

3. **Follow the Journey**: Start with the [Business Case](https://maximilianoPizarro.github.io/rhoai-roadshow-from-zero-to-hero/#/0-getting-connected/0-business-case) and work through each section

## 📚 Documentation Structure

```
docs/
├── 0-getting-connected/          # Environment setup and business case
│   ├── 0-business-case.md
│   ├── 0.5-workshop-overview.md
│   └── 2-configure-environment.md
├── 3-agents-tools/               # MCP Agents development
│   ├── 0-intro.md               # MCP and LlamaStack introduction
│   ├── 1-golden-path.md         # Developer Hub and Software Templates
│   ├── 2-devspaces.md           # Working with DevSpaces
│   ├── 2.5-keycloak-user-management.md
│   ├── 3-build-mcp-agent.md     # Building the MCP agent
│   ├── 3.5-connectivity-link.md # Service mesh communication
│   ├── 4-mcp-inspector.md       # Testing with MCP Inspector
│   ├── 5-deploy-integrate.md    # Integration with Playground
│   └── 6-opentelemetry.md       # Observability
└── 6-resources/                  # Additional resources
```

## 🎓 Target Audience

This workshop is designed for:

- **Application Developers**: Building AI-powered applications and agentic systems
- **Platform Engineers**: Providing infrastructure and Golden Paths for developers
- **DevOps Engineers**: Automating AI/ML operations and deployments
- **Security Professionals**: Understanding guardrails and compliance for AI systems

## 🔗 Key Resources

- **Documentation**: [https://maximilianoPizarro.github.io/rhoai-roadshow-from-zero-to-hero/](https://maximilianoPizarro.github.io/rhoai-roadshow-from-zero-to-hero/)
- **Source Code**: [https://github.com/maximilianoPizarro/rhoai-roadshow-from-zero-to-hero](https://github.com/maximilianoPizarro/rhoai-roadshow-from-zero-to-hero)
- **Ansible Setup**: [https://github.com/panchoraposo/rh1-demo](https://github.com/panchoraposo/rh1-demo)
- **Neuralbank Workshop**: [https://github.com/pkstaz/neuralbank-workshop](https://github.com/pkstaz/neuralbank-workshop)
- **Helm Chart**: [https://github.com/maximilianoPizarro/neuralbank-stack](https://github.com/maximilianoPizarro/neuralbank-stack)
- **Connectivity Link**: [https://maximilianopizarro.github.io/connectivity-link/](https://maximilianopizarro.github.io/connectivity-link/)

## ✅ Success Criteria

By completing this workshop, you will have:

✅ Built and deployed an MCP Agent on OpenShift  
✅ Integrated with enterprise authentication (Keycloak)  
✅ Connected services via Connectivity Link  
✅ Enabled chat-based interaction through Playground  
✅ Implemented full observability with OpenTelemetry  
✅ Understood best practices for AI/ML development on OpenShift  

## 📝 License

This workshop content is provided for educational purposes.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/maximilianoPizarro/rhoai-roadshow-from-zero-to-hero/issues).

---

**Ready to start your journey?** Visit the [documentation](https://maximilianoPizarro.github.io/rhoai-roadshow-from-zero-to-hero/) and begin with the [Business Case](https://maximilianoPizarro.github.io/rhoai-roadshow-from-zero-to-hero/#/0-getting-connected/0-business-case)!
