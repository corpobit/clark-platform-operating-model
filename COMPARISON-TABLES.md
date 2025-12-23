# Clark Platform - Comparison Tables

## Baseline Repositories

| Repository | Technology | Purpose | Ownership | Managed By | What It Manages |
|------------|------------|---------|-----------|------------|-----------------|
| `clark-platform-infra` | Terraform | Foundational infrastructure | Customer | Clark | Cloud accounts, networking, Kubernetes clusters, IAM, monitoring baselines |
| `clark-platform-control` | Crossplane | Cloud service control plane | Customer | Clark | Databases, storage, queues, managed services, platform GitOps |

## What's Included vs. Not Included

| Category | Included in Baseline | Not Included (Optional) |
|----------|---------------------|------------------------|
| **Infrastructure** | ✅ Cloud accounts, networking, Kubernetes clusters | ❌ Application infrastructure |
| **Control Plane** | ✅ Crossplane installation and management | ❌ Application control planes |
| **GitOps** | ✅ Platform GitOps (infrastructure) | ❌ Application GitOps (optional) |
| **Monitoring** | ✅ Infrastructure monitoring baseline | ❌ Application monitoring (optional) |
| **Secrets** | ❌ | ✅ Secrets management (optional) |
| **CI/CD** | ❌ | ✅ CI/CD pipelines (optional) |
| **Observability** | ✅ Basic monitoring | ✅ Advanced observability (optional) |
| **Security** | ✅ Infrastructure security | ✅ Advanced security tools (optional) |

## Control Boundaries Matrix

| Area | Customer | Clark | Notes |
|------|----------|-------|-------|
| **Cloud Accounts** | ✅ Owns | ❌ | Customer has full control |
| **Infrastructure Code** | ✅ Owns | ✅ Maintains | Customer owns, Clark maintains |
| **Crossplane Compositions** | ✅ Owns | ✅ Maintains | Customer owns, Clark maintains |
| **Application Code** | ✅ Owns | ❌ | Customer responsibility |
| **CI/CD** | ✅ Owns | Optional | Customer owns, Clark can support |
| **Exit Capability** | ✅ Always | ✅ Guaranteed | No lock-in, exit anytime |

## GitOps Layers Comparison

| Aspect | Platform GitOps | Application GitOps |
|--------|----------------|-------------------|
| **Purpose** | Infrastructure & cloud services | Application deployments |
| **Owned By** | Customer | Customer |
| **Managed By** | Clark | Customer teams |
| **Repository** | `clark-platform-control` | Customer application repos |
| **Technology** | Crossplane | ArgoCD/Flux (optional) |
| **Workflow** | PR → Clark Review → Apply | PR → Customer Review → Apply |
| **Scope** | Cloud resources | Application code |

## Optional Services Comparison

| Service Category | Options | Setup Time | Monthly Cost | Use Case |
|-----------------|---------|------------|--------------|----------|
| **Secrets Management** | AWS Secrets Manager, Azure Key Vault, GCP Secret Manager, Vault | 1-2 weeks | Medium | Centralized secret storage |
| **Application GitOps** | ArgoCD, Flux | 1-2 weeks | Low | GitOps for applications |
| **CI/CD Pipelines** | GitHub Actions, GitLab CI, Bitbucket | 1-2 weeks | Low | Standardized pipelines |
| **Observability** | Prometheus, Grafana, Cloud-native | 2-3 weeks | Medium | Advanced monitoring |
| **Security Tools** | OPA, Kyverno, Cloud-native | 1-2 weeks | Low | Policy enforcement |

## Onboarding Timeline

| Phase | Duration | Activities | Deliverables |
|-------|----------|------------|--------------|
| **Setup & Preparation** | Week 1 | Account setup, repository cloning, requirements gathering | Configured repositories |
| **Infrastructure Provisioning** | Week 2-3 | Network setup, Kubernetes cluster, IAM, monitoring | Provisioned infrastructure |
| **Control Plane & Training** | Week 3-4 | Crossplane installation, GitOps setup, training | Operational platform |
| **Stabilization** | Week 5-8 | Monitoring, optimization, support | Stable platform |

## Exit Process Comparison

| Aspect | Standard Exit | Accelerated Exit |
|--------|---------------|-----------------|
| **Timeline** | 2-4 weeks | 1-2 weeks |
| **Knowledge Transfer** | Comprehensive | Focused |
| **Training** | Full training sessions | Essential training only |
| **Support** | Transition support included | Minimal support |
| **Best For** | Teams building capability | Teams with existing expertise |

## Service Models Comparison

| Aspect | Full Managed | Co-Managed | Consulting Only |
|--------|-------------|------------|-----------------|
| **Operations** | Clark handles all | Shared responsibility | Customer handles |
| **Support** | 24/7 | Business hours | Limited |
| **Training** | Included | Included | Included |
| **Best For** | No platform expertise | Building capability | Existing expertise |
| **Cost** | Higher | Medium | Lower |

## Technology Stack

| Layer | Technology | Purpose | Provider |
|-------|------------|---------|----------|
| **Infrastructure** | Terraform | Infrastructure provisioning | HashiCorp |
| **Control Plane** | Crossplane | Cloud service management | CNCF |
| **Orchestration** | Kubernetes | Container orchestration | CNCF |
| **GitOps** | Git | Version control and workflows | Various |
| **Cloud Providers** | AWS, GCP, Azure | Cloud infrastructure | Various |

## Repository Access Levels

| Role | clark-platform-infra | clark-platform-control | Application Repos |
|------|----------------------|------------------------|------------------|
| **Customer** | Owner | Owner | Owner |
| **Clark** | Maintainer | Maintainer | No access (unless support) |
| **Development Teams** | Read (optional) | Contributor | Full access |

## Responsibility Matrix Summary

| Responsibility | Customer | Clark | Shared |
|----------------|----------|-------|--------|
| **Cloud Account Ownership** | ✅ | ❌ | ❌ |
| **Infrastructure Provisioning** | ❌ | ✅ | ❌ |
| **Control Plane Management** | ❌ | ✅ | ❌ |
| **Application Development** | ✅ | ❌ | ❌ |
| **Security Policies** | ❌ | ❌ | ✅ |
| **Cost Management** | ❌ | ❌ | ✅ |
| **Compliance** | ❌ | ❌ | ✅ |
| **Documentation** | ❌ | ✅ | ❌ |
| **Training** | ❌ | ✅ | ❌ |
| **Support** | ❌ | ✅ | ❌ |

## Pricing Model Comparison

| Model | Setup Cost | Monthly Cost | Best For |
|-------|------------|--------------|----------|
| **Baseline Service** | Included | Based on scale | All customers |
| **Optional Services** | One-time fee | Monthly maintenance | Specific needs |
| **Enterprise** | Custom | Custom | Large scale |

## Security Model

| Aspect | Customer Responsibility | Clark Responsibility | Shared |
|--------|------------------------|---------------------|--------|
| **Cloud Account Security** | ✅ Owns | ✅ Configures | ✅ |
| **Repository Access** | ✅ Controls | ✅ Has access | ✅ |
| **Kubernetes Access** | ✅ Controls | ✅ Has access | ✅ |
| **Secret Management** | ✅ Owns | Optional support | ❌ |
| **Compliance** | ✅ Approves | ✅ Implements | ✅ |
| **Security Audits** | ✅ Participates | ✅ Participates | ✅ |

## Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Time to Production** | 4 weeks | Onboarding completion |
| **Infrastructure Availability** | 99.9% | Uptime monitoring |
| **Change Request Turnaround** | < 24 hours | PR review time |
| **Customer Satisfaction** | High | Regular surveys |
| **Exit Success** | 100% | Successful transitions |

## Decision Authority

| Decision Type | Customer | Clark | Joint |
|---------------|----------|-------|-------|
| **Cloud Provider Selection** | ✅ | ❌ | ❌ |
| **Resource Sizing** | ✅ | ❌ | ❌ |
| **Architecture Patterns** | ❌ | ✅ | ❌ |
| **Policy Definitions** | ❌ | ✅ | ❌ |
| **New Service Additions** | ❌ | ❌ | ✅ |
| **Major Changes** | ❌ | ❌ | ✅ |
| **Cost Budgets** | ✅ | ❌ | ❌ |
| **Team Access** | ✅ | ❌ | ❌ |

