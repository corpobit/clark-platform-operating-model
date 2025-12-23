# Clark Platform - Executive Summary

## One-Page Overview

### What is Clark?

Clark is a managed platform engineering service that provisions and operates cloud infrastructure using Infrastructure-as-Code and GitOps, while customers retain full ownership of their cloud accounts, repositories, and systems.

### Core Value Proposition

**Clark provides structure, safety, and speed — not control.**

We operate as an embedded platform team, not a vendor-controlled layer.

### Two Core Repositories

| Repository | Purpose | Ownership |
|------------|---------|-----------|
| `clark-platform-infra` | Foundational infrastructure via Terraform | Customer owns, Clark operates |
| `clark-platform-control` | Cloud services via Crossplane | Customer owns, Clark operates |

### What's Included (Baseline)

✅ Cloud account setup and configuration
✅ Networking (VPC/VNet, subnets, routing)
✅ Kubernetes cluster provisioning
✅ IAM and access boundaries
✅ Logging and monitoring baselines
✅ Crossplane control plane
✅ Platform GitOps workflows
✅ Documentation and training
✅ Standard support

### What's NOT Included

❌ Application deployments
❌ Application CI/CD (optional)
❌ Application monitoring (optional)
❌ Business logic

### Optional Services

- **Secrets Management**: AWS Secrets Manager, Azure Key Vault, Vault
- **Application GitOps**: ArgoCD, Flux
- **CI/CD**: GitHub Actions, GitLab CI
- **Observability**: Prometheus, Grafana
- **Security**: OPA, Kyverno

### Control Boundaries

| Area | Customer | Clark |
|------|----------|-------|
| Cloud accounts | ✅ Owns | ❌ |
| Infrastructure code | ✅ Owns | ✅ Maintains |
| Application code | ✅ Owns | ❌ |
| Exit capability | ✅ Always | ✅ Guaranteed |

### Key Principles

1. **Customer Ownership**: Customers own everything
2. **Clark Operation**: Clark maintains and operates
3. **No Lock-In**: Exit anytime, no penalties
4. **Clear Boundaries**: Platform vs. application separation
5. **Trust Through Ownership**: We operate, you own

### Onboarding

**Timeline**: 4 weeks to production
- Week 1: Setup and preparation
- Week 2-3: Infrastructure provisioning
- Week 3-4: Control plane and training
- Week 5-8: Stabilization

### Exit Strategy

- **Always Available**: Exit anytime
- **No Lock-In**: No penalties or lock-in periods
- **Full Transfer**: Complete knowledge and access transfer
- **Timeline**: 2-4 weeks standard

### Why Clark?

🚀 **Speed**: Weeks to production, not months
🛡️ **Safety**: Best practices built-in
💰 **Cost Effective**: No hiring or training costs
🎯 **Focus**: You build product, we manage platform

### Target Customers

- Early-stage startups needing infrastructure fast
- Growing companies scaling infrastructure
- Teams building platform capability
- Companies wanting expert platform operations

### Technology Stack

- **Infrastructure**: Terraform
- **Control Plane**: Crossplane
- **Orchestration**: Kubernetes
- **GitOps**: Git-driven workflows
- **Cloud Providers**: AWS, GCP, Azure

### Pricing Model

- **Baseline**: Monthly subscription based on scale
- **Optional Services**: Setup fee + monthly maintenance
- **Transparent**: No hidden costs
- **Predictable**: Fixed monthly costs

### Documentation Structure

1. Overview
2. Architecture
3. Repository Model
4. GitOps Model
5. Responsibility Matrix
6. Onboarding Process
7. Optional Services
8. Security and Access
9. Ownership and Exit
10. Pricing and Engagement

### Next Steps

1. Review [Overview](01-overview.md) for detailed introduction
2. Check [Architecture](02-architecture.md) for technical details
3. Read [Presentation](presentation.md) for sales deck
4. Contact Clark team for discussion

---

**Clark Platform**: Managed Platform Engineering with Full Customer Ownership

