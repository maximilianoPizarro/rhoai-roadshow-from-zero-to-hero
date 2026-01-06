# 🏦 Neuralbank Business Case

## Overview

**Neuralbank** is a forward-thinking financial institution that provides loans to customers. Like many financial organizations, Neuralbank faces challenges in accelerating credit decisions while maintaining compliance and transparency.

## The Problem

Currently, customers experience significant delays when applying for loans. The bottleneck occurs in the **credit risk assessment process**:

1. **Manual Risk Updates**: Credit risk levels must be manually updated by analysts
2. **Time Delays**: The manual process creates delays in credit approval
3. **Compliance Requirements**: All operations must be transparent and auditable
4. **Scalability Issues**: As the institution grows, manual processes don't scale

## The Solution: MCP Agents

To solve this challenge, Neuralbank is implementing an **MCP (Model Context Protocol) Agent** that:

- **Queries Credit Risk**: Commercial agents can query customer credit risk information via a chat interface
- **Updates Risk Levels**: Automatically updates credit risk levels based on loan requests
- **Accelerates Decisions**: Reduces approval time from days to minutes
- **Maintains Compliance**: Provides transparent, auditable operations with full traceability

## Architecture Overview

Neuralbank's infrastructure includes:

```
┌─────────────────────────────────────────────────────────┐
│                    Frontend Layer                        │
│  (Customer Portal, Commercial Agent Interface)          │
└────────────────────┬────────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────────┐
│              Authentication Layer                        │
│                    Keycloak                             │
└────────────────────┬────────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────────┐
│              Backend Services (Java)                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐ │
│  │ Credit Risk  │  │ Loan Service │  │ MCP Agent    │ │
│  │   Service    │  │              │  │              │ │
│  └──────────────┘  └──────────────┘  └──────────────┘ │
└────────────────────┬────────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────────┐
│            Connectivity Link                            │
│        (Service Integration Layer)                      │
└─────────────────────────────────────────────────────────┘
```

## Your Role as Kevin

As a new Java developer joining Neuralbank, you will:

1. **Understand the Architecture**: Learn about Neuralbank's frontend/backend architecture with Keycloak and Connectivity Link
2. **Work with the Golden Path**: Use the Platform Engineering team's pre-configured development environment
3. **Build the MCP Agent**: Develop and deploy the agent that queries and updates credit risk
4. **Test and Validate**: Use MCP Inspector and Cursor to verify functionality
5. **Integrate with Frontend**: Ensure commercial agents can use the chat interface
6. **Monitor Operations**: Use OpenTelemetry to observe distributed traces

## Success Criteria

By the end of this journey, you will have:

✅ A working MCP Agent deployed on OpenShift  
✅ Integration with Neuralbank's credit risk system  
✅ A chat interface for commercial agents  
✅ Full observability with OpenTelemetry traces  
✅ Understanding of best practices for AI/ML on OpenShift  

## Next Steps

Ready to begin? Let's start by [getting connected](1-get-connected.md) to your OpenShift AI environment.

