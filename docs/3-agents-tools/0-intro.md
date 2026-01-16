# 🎯 Introduction to MCP Agents

?> **Access Note**: To access the OpenShift console and observe the architecture, authenticate using:
- **OpenShift Console**: <a href="https://console-openshift-console.apps.<CLUSTER_DOMAIN>" target="_blank">https://console-openshift-console.apps.<CLUSTER_DOMAIN></a>
- **Username**: `admin`
- **Password**: `Welcome123`

## What is MCP?

**Model Context Protocol (MCP)** is an open protocol that enables AI assistants to securely access external data sources and tools. MCP servers provide a standardized way for AI applications to interact with various services, databases, and APIs.

For Neuralbank, MCP Agents serve as intelligent intermediaries that:

- **Query Credit Risk Data**: Retrieve customer credit risk information from backend services
- **Update Risk Levels**: Modify credit risk assessments based on loan requests
- **Provide Transparency**: Maintain audit trails for compliance
- **Accelerate Decisions**: Automate manual processes to speed up loan approvals

## LlamaStack Overview

**LlamaStack** is an open-source framework for building production-ready generative AI applications on Kubernetes. It provides a comprehensive, enterprise-grade platform for deploying, managing, and orchestrating Large Language Models (LLMs), tools, agents, and MCP servers at scale.

<img src="../images/llama-stack.png" alt="LlamaStack Overview" width="50%" style="display: block; margin: 0 auto;">

> **Reference**: This section is based on insights from the Red Hat blog post: ["Llama Stack and the case for an open 'run-anywhere' contract for agents"](https://www.redhat.com/en/blog/llama-stack-and-case-open-run-anywhere-contract-agents)

### The 4 Layers of LlamaStack

LlamaStack is better understood as four distinct layers, rather than just another agent framework:

#### 1. Build Layer (Client SDK/Toolkit)
A familiar surface for building agents, similar to LangChain, LangFlow, and CrewAI. Developers can author agents using common abstractions. The agent artifacts (YAML configs, Python tasks, tool bindings) are portable across environments.

#### 2. Agent Artifacts and Dependencies
The tangible artifacts of agent development that need runtimes and API endpoints for model inference, tool calling, safety, and telemetry. LlamaStack enables both local development and remote endpoint deployments, ensuring artifacts run consistently regardless of backend models or tools.

#### 3. Platform / API Layer
A standardized API surface for core AI services, including inference, memory, tool use, post-training, data and synthetic generation, and evaluation. LlamaStack has built-in support for:
- **OpenAI-compatible APIs**: One of the few open implementations of OpenAI's APIs (Chat Completions, Responses API, file_search, vectorstores, and more)
- **Model Context Protocol (MCP)**: Open protocol for tool calling and standardized communication
- **Extended APIs**: Beyond OpenAI APIs for eval, fine-tuning, model-customization, scoring, and dataset management

#### 4. Provider Model
A plugin system for backends—whether open source or proprietary. This allows you to swap model providers, vector databases, or runtime implementations without touching agent code. Your agent logic remains unchanged while infrastructure can be swapped.

### The Kubernetes Analogy

Much like Kubernetes defined a **control plane + plugin contract** (CNI for networking, CSI for storage, CRI for runtimes) that enabled portability across vendors and clouds, **LlamaStack aims to be the "run-anywhere contract" for agents**:

- **For developers**: The APIs you use and artifacts you produce should run without change across environments
- **For platforms**: The underlying infrastructure (models, vector databases, training runtimes, tool APIs) should be pluggable providers

Think of Kubernetes orchestrating containers, and LlamaStack orchestrating agents and their providers.

### Core Capabilities

LlamaStack offers a complete ecosystem for AI application development:

- **Multiple Model Support**: Seamlessly integrate and switch between various LLM models (Llama, DeepSeek, Mistral, and more) through a unified interface
- **RAG (Retrieval Augmented Generation)**: Built-in vector database support with automatic embedding generation, enabling context-aware responses from your knowledge base
- **Tools and Agents Framework**: Extensible tool system that allows you to create custom functions and chain them together for complex workflows
- **MCP (Model Context Protocol) Integration**: Native support for MCP servers, enabling standardized communication between AI assistants and external data sources
- **Playground Interface**: Interactive web-based UI for testing, debugging, and developing AI applications without writing code
- **Kubernetes-Native**: Designed for OpenShift/Kubernetes, providing scalability, reliability, and enterprise security features
- **Observability**: Built-in monitoring, logging, and tracing capabilities for production deployments

### Architecture Benefits

LlamaStack's architecture provides several advantages for enterprise AI deployments:

- **Microservices-Based**: Modular design allows independent scaling of components (models, tools, agents)
- **API-First**: RESTful and streaming APIs for easy integration with existing systems
- **Security**: Role-based access control, authentication, and secure communication channels
- **High Availability**: Designed for 99.9% uptime with health checks, auto-recovery, and load balancing
- **Resource Management**: Efficient GPU and CPU utilization with intelligent workload scheduling
- **Open Standards**: Supports both OpenAI-compatible APIs (for compatibility) and open standards like MCP (for vendor independence)

### Integration with Neuralbank

The Neuralbank MCP Agent integrates seamlessly with LlamaStack's Playground, creating a powerful workflow:

1. **Commercial agents** interact with the system through LlamaStack's intuitive chat interface
2. **LlamaStack** routes requests to the MCP Agent using the Model Context Protocol
3. **MCP Agent** processes queries and interacts with Neuralbank's backend services
4. **Results** flow back through LlamaStack to provide real-time responses to commercial agents

This integration enables commercial agents to:
- Query customer credit risk information in natural language
- Update risk levels based on loan application parameters
- Get instant feedback on credit decisions
- Maintain full audit trails for compliance

The combination of LlamaStack's AI capabilities and MCP's standardized protocol creates a robust, scalable solution for Neuralbank's credit risk management needs.

## The Neuralbank MCP Agent

The MCP Agent you'll build will:

1. **Receive Queries**: Commercial agents query customer credit risk via chat interface
2. **Process Requests**: The MCP Agent processes the query and determines required actions
3. **Interact with Services**: Connects to Neuralbank's credit risk service via Connectivity Link
4. **Update Risk Levels**: Modifies credit risk based on loan request parameters
5. **Return Results**: Provides updated information back to the commercial agent

## Neuralbank Architecture

The Neuralbank topology is already installed in your environment. The complete architecture includes:

- **Frontend Services**: Customer and commercial agent interfaces
- **Authentication Layer**: Keycloak for identity management
- **Backend Services**: Credit risk and loan management services
- **Connectivity Link**: Service mesh for secure communication
- **MCP Agent**: The `customer-service-mcp` service you'll develop

<img src="../images/neuralbank-tology-connectivity-link.png" alt="Neuralbank Topology with Connectivity Link" style="max-width: 80%; display: block; margin: 20px auto;">

?> **Note**: The complete Neuralbank topology diagram is available in the [Resources section](6-resources/README) under Helm Chart deployment.

## Architecture Flow

```
Commercial Agent (Frontend/Playground)
         │
         │ Chat Query: "Update credit risk for customer X"
         │ (Authenticated via Keycloak)
         ▼
    LlamaStack Playground
         │
         │ MCP Protocol Request
         ▼
    customer-service-mcp (OpenShift)
         │
         │ Query Credit Risk Service via Connectivity Link
         ▼
    Credit Risk Service (Backend)
         │
         │ Update Risk Level
         ▼
    Database
         │
         │ Return Updated Risk
         ▼
    customer-service-mcp
         │
         │ Return Result via MCP
         ▼
    LlamaStack Playground
         │
         │ Display Result
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

<input type="checkbox" id="benefit1" checked> <label for="benefit1">**Faster Decisions**: Reduce credit approval time from days to minutes</label>  
<input type="checkbox" id="benefit2" checked> <label for="benefit2">**Scalability**: Handle increasing loan volumes without proportional staff increases</label>  
<input type="checkbox" id="benefit3" checked> <label for="benefit3">**Compliance**: Full audit trail of all operations</label>  
<input type="checkbox" id="benefit4" checked> <label for="benefit4">**Transparency**: Clear visibility into risk assessment changes</label>  
<input type="checkbox" id="benefit5" checked> <label for="benefit5">**Developer Experience**: Easy to develop, test, and deploy using Golden Path</label>  

## What's Next?

Now that you understand the basics, let's explore the **Golden Path** that the Platform Engineering team has prepared for you. This will make it easy to get started with your development environment.

Click **Golden Path & Developer Hub** to continue.
