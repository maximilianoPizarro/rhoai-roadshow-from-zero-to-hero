# Red Hat OpenShift AI From Zero To Hero

This repo contains the **Red Hat OpenShift AI From Zero To Hero** workshop - a comprehensive journey from business use case to production-ready AI solution.

The instructions for the workshop are located under the `docs` directory.  

To start the document server, follow the instructions [here](https://github.com/maximilianoPizarro/rhoai-roadshow-from-zero-to-hero/blob/main/site/README.md).

## Vision

The roadshow v2 is intended to provide short-sharp use-case (pattern)-centric labs to showcase everything that differentiates Red Hat OpenSHift AI and makes it unique.

It will be relevant to the kinds of problems that teams want to do with generative and/or predictive/classificatory (traditional) AI.

## Target audience

The roadshow will provide value to multiple personas:

1. Platform engineers that need to provide:
   a. The software infrastructure that data scientists and application developers need to build intelligent applications  
   b. Model as a service or GPU as a service to their internal customers.  

2. Data scientists and data engineers and domain experts that need to prepare data for training of RAG-based solutions, and validate their performance.

3. Application developers that need to:
  a. Experiment with traditional AI/ML models and LLMs and integrate them with their intelligent applications.  
  b. Build agentic systems.

4. DevOps engineers that need to automate GenAIOps and AIMLOps and provide auditable baseline management.  

5. Security and compliance professionals that need to ensure there are effective guardrails around the use of generative AI.

## Roadshow format

* Self contained labs designed to showcase a defined set of RHOAI features and noteworthy patterns that everyone is excited about.
* Modules not interconnected.
* Delivery format: Based on the TL500/ML500 course.
* Labs timeboxed to an hour max each
* "Follow the bouncing ball" style

## Content

This workshop focuses on building MCP Agents for Neuralbank, a financial institution use case, covering:

- **OpenShift AI Setup**: Getting connected and configuring your environment
- **MCP Agents**: Building and deploying agents for credit risk management
- **Models**: Working with Red Hat AI Inference Server (RHAIIS) for model serving
- **Observability**: Monitoring with OpenTelemetry distributed traces
