# 📚 Resources

This section provides additional resources and alternative installation methods for the Neuralbank workshop and infrastructure setup.

## Source Code

### Neuralbank Workshop Repository

The complete source code for the Neuralbank workshop, including all services, MCP agents, and frontend components.

🔗 **Repository**: [https://github.com/pkstaz/neuralbank-workshop](https://github.com/pkstaz/neuralbank-workshop)

This repository contains:
- `customer-service` - Backend service implemented in Java (Maven)
- `customer-service-mcp` - Workshop code and exercises
- `credit-approval-service` - Credit approval microservice
- `credit-approval-mcp` - Workshop variant of credit approval code
- `neuralbank-front` - Customer-facing UI (Node/TypeScript)
- `database` - SQL scripts and DB resources
- `charts` - Helm chart for deploying the core stack

## Installation Methods

### Ansible Setup

Automated deployment using Ansible playbooks for a complete Internal Developer Platform (IDP) setup on Red Hat OpenShift.

🔗 **Repository**: [https://github.com/panchoraposo/rh1-demo](https://github.com/panchoraposo/rh1-demo)

This Ansible-based setup provisions:
- OpenShift GitOps (Argo CD)
- Keycloak for identity management
- HashiCorp Vault + External Secrets Operator
- GitLab + OpenShift Pipelines
- Red Hat Developer Hub
- Quay & ODF (OpenShift Data Foundation)
- OpenShift Dev Spaces
- Full observability and logging stack

**Installation Time**: ~40 minutes

### Helm Chart

Deploy the Neuralbank stack using Helm charts for quick and easy setup.

🔗 **Repository**: [https://github.com/maximilianoPizarro/neuralbank-stack](https://github.com/maximilianoPizarro/neuralbank-stack)

The Helm chart includes:
- Pre-configured services
- Database setup
- Nginx proxy configuration
- All required dependencies

### GitOps with ArgoCD

Alternative installation path using GitOps principles with ArgoCD for declarative infrastructure management.

🔗 **Documentation**: [https://maximilianopizarro.github.io/connectivity-link/](https://maximilianopizarro.github.io/connectivity-link/)

This GitOps approach provides:
- Declarative infrastructure management
- Automated synchronization
- Version control for all configurations
- Connectivity Link integration
- Continuous deployment workflows

## Additional Resources

### Documentation

- **Red Hat OpenShift AI**: [Official Documentation](https://access.redhat.com/documentation/en-us/red_hat_openshift_ai)
- **Model Context Protocol**: [MCP Specification](https://modelcontextprotocol.io)
- **LlamaStack**: [Documentation](https://llama-stack.readthedocs.io)
- **Red Hat Developer Hub**: [Documentation](https://access.redhat.com/documentation/en-us/red_hat_developer_hub)

### Community

- **Red Hat Community**: Join discussions and get support
- **GitHub Discussions**: Participate in repository discussions
- **Red Hat Events**: Attend workshops and webinars

## Quick Links

| Resource | Description | Link |
|----------|------------|------|
| **Source Code** | Complete Neuralbank workshop code | [neuralbank-workshop](https://github.com/pkstaz/neuralbank-workshop) |
| **Ansible Setup** | Automated IDP deployment | [rh1-demo](https://github.com/panchoraposo/rh1-demo) |
| **Helm Chart** | Quick deployment option | [neuralbank-stack](https://github.com/maximilianoPizarro/neuralbank-stack) |
| **GitOps Guide** | ArgoCD installation path | [connectivity-link](https://maximilianopizarro.github.io/connectivity-link/) |

## Choosing the Right Installation Method

- **Ansible Setup**: Best for complete platform setup with all components
- **Helm Chart**: Quickest way to deploy the Neuralbank stack
- **GitOps/ArgoCD**: Ideal for teams using GitOps workflows and declarative infrastructure
- **Manual Setup**: Follow the step-by-step guide in this documentation

## Support

For issues, questions, or contributions:
- Open an issue in the respective repository
- Check existing documentation
- Reach out to the community

