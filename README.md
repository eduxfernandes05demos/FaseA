# Modernizing a Monolith

> **Transforming a C and Assembly monolith into a cloud-native, microservices-based modern platform**

[![License](https://img.shields.io/badge/license-GPL-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Azure-0078D4.svg)](https://azure.microsoft.com)
[![Architecture](https://img.shields.io/badge/architecture-Microservices-brightgreen.svg)](docs/architecture.md)

## Project Vision

This project demonstrates the modernization journey of a 30-year-old codebase, transforming a monolithic C architecture into a distributed, cloud-native application. Our goal is to showcase how legacy applications can be reimagined using modern development practices, AI-assisted refactoring, and cloud infrastructure.

## Objectives

- **Decompose** the monolithic engine into independent, scalable microservices
- **Modernize** the codebase using contemporary programming languages and frameworks
- **Containerize** services for cloud deployment and orchestration
- **Enhance** with real-time telemetry, monitoring, and observability
- **Secure** the architecture with modern authentication and security practices
- **Scale** the platform to support high-throughput, distributed workloads

## Architecture Overview

```
Browser (WebRTC)
    |
    v
+------------------+     +------------------+
| Streaming Gateway|---->|   Engine Worker   |
|   (Go, :8090)    |     | (Headless C App)  |
| WebSocket signal |     |  RGBA framebuffer |
| + HTML client    |     |  :8080 /healthz   |
+------------------+     +------------------+
    |                          |
    v                          v
+------------------+     +------------------+
| Session Manager  |     |  Telemetry API   |
|   (Go, :8080)    |     |   (Go, :8060)    |
| POST/GET/DELETE  |     | -> App Insights  |
| /api/sessions    |     | /api/events      |
+------------------+     +------------------+
    |
    v
+------------------+
|   Assets API     |
|   (Go, :8070)    |
| Static content   |
| /api/assets/     |
+------------------+
```

### Services

1. **Streaming Gateway** (Go, port 8090) - WebSocket signaling server for WebRTC connection setup, frame encoding (VP8/H.264), HTML client serving, and input routing
2. **Engine Worker** (C, port 8080) - Headless modernized engine producing RGBA framebuffer output, with health endpoint at `/healthz` and environment-based configuration
3. **Session Manager** (Go, port 8080) - REST API for session lifecycle (`POST/GET/DELETE /api/sessions`), instance creation/destruction, health monitoring, scale-to-zero support
4. **Assets API** (Go, port 8070) - Static content server reading from Azure Files mount, with caching headers for asset delivery
5. **Telemetry API** (Go, port 8060) - Event ingestion (`POST /api/events`) forwarding to Azure Application Insights, structured logging and metrics

## Technology Stack

- **Languages**: C (engine), Go (services), Bicep (IaC)
- **Containerization**: Docker, Azure Container Apps
- **Cloud Platform**: Microsoft Azure
- **Streaming**: WebRTC, WebSocket signaling
- **Storage**: Azure Files
- **Secrets**: Azure Key Vault (RBAC auth)
- **Monitoring**: Application Insights, Log Analytics
- **Registry**: Azure Container Registry
- **CI/CD**: GitHub Actions

## The Transformation

### Scenario 1: From Monolith to Microservices
Live-refactor portions of the original C codebase into modern, containerized services. AI-assisted code generation with Copilot helps translate legacy patterns into cloud-native architectures.

### Scenario 2: Real-Time Scalability
Spin up multiple service instances dynamically using container orchestration. Auto-scaling as load increases, with scale-to-zero for idle workers.

### Scenario 3: Observability & Telemetry
Live dashboards showing real-time metrics: processing throughput, network latency, and service health. Distributed tracing follows requests across multiple microservices.

### Scenario 4: Security Modernization
Zero-trust principles protecting the infrastructure. Authentication flows, service-to-service authorization, and threat detection using Azure Security Center.

### Scenario 5: AI-Powered Development
AI pair programming accelerates modernization. GitHub Copilot suggests optimizations and helps navigate 90,000+ lines of legacy code.

### Comparison

| Feature | Legacy Monolith | Modernized Platform |
|---------|----------------|---------------------|
| **Architecture** | Monolithic C binary | 5 distributed microservices |
| **Deployment** | Manual setup | Containerized on Azure Container Apps |
| **Scaling** | Single server limit | Horizontal auto-scaling (0 to N) |
| **Monitoring** | Console logs | App Insights + Log Analytics |
| **Updates** | Full restart required | Zero-downtime deployments |
| **Security** | Basic network security | Key Vault + RBAC + zero-trust |
| **Access** | Local binary only | Browser via WebRTC streaming |

### Technical Innovations

- **Headless Engine**: Legacy rendering replaced with framebuffer output for cloud streaming
- **WebRTC Streaming**: Real-time browser access without client installation
- **Event-Driven Design**: Real-time state synchronization across distributed systems
- **Scale-to-Zero**: No idle cost  workers scale down when unused
- **GitOps Workflows**: Infrastructure as Code with automated deployments
- **AI Collaboration**: Human + AI partnership in legacy code modernization

## Azure Resources

| Resource | Purpose |
|----------|---------|
| Azure Container Registry | Stores container images |
| Azure Container Apps Environment | Hosts all containers |
| Engine Worker Container App | Headless engine (0 to N replicas) |
| Azure Files | Persistent storage for assets |
| Azure Key Vault | Secrets management (RBAC auth) |
| Application Insights + Log Analytics | Monitoring and telemetry |

## Getting Started

### Prerequisites

- Docker Desktop
- Azure CLI
- Git
- Visual Studio Code with relevant extensions

### Quick Start

```bash
# Clone the repository
git clone https://github.com/eduxfernandes05/FaseA.git
cd FaseA

# Run local development environment
docker-compose up -d
```

## Contributing

This is a demonstration project, but feedback and suggestions are welcome! Feel free to open issues or submit pull requests.

## License

Licensed under GPL-2.0.

---

**Built with passion for software modernization and cloud architecture**