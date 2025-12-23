# Clark Platform - Overview

## Executive Summary

Clark is a managed platform engineering service. We provision and operate cloud infrastructure using Infrastructure-as-Code and GitOps, while customers retain full ownership of their cloud accounts, repositories, and systems.

## Core Value Proposition

Clark provides structure, safety, and speed — not control. We operate as an embedded platform team, not a vendor-controlled layer.

## The Problem

Early-stage startups and growing companies face significant challenges:

- **Infrastructure Complexity**: Managing cloud infrastructure requires deep expertise
- **Time to Market**: Building platform capabilities diverts focus from product development
- **Operational Overhead**: Maintaining infrastructure-as-code and GitOps requires dedicated resources
- **Knowledge Gap**: Platform engineering requires specialized skills that are expensive to hire

## The Clark Solution

Clark delivers a managed platform engineering service that:

1. **Provisions Infrastructure**: Sets up and maintains cloud infrastructure using Terraform
2. **Operates Control Plane**: Manages cloud services via Crossplane
3. **Maintains GitOps**: Ensures infrastructure changes follow GitOps best practices
4. **Preserves Ownership**: Customers retain full ownership and control

## Core Baseline

Clark has exactly two mandatory technical pillars at the start:

### Baseline Repositories (per customer)

| Repository | Purpose | Ownership |
|------------|---------|-----------|
| `clark-platform-infra` | Foundational infrastructure via Terraform | Customer (operated by Clark) |
| `clark-platform-control` | Cloud service control plane via Crossplane | Customer (operated by Clark) |

These two repositories are:
- Cloned per customer
- Fully owned by the customer
- Maintained by Clark under contract

## What Clark Does

### Included in Baseline

- Cloud account setup and configuration
- Networking (VPC/VNet, subnets, routing)
- Kubernetes cluster provisioning
- IAM and access boundaries
- Logging and monitoring baselines
- Terraform state management
- Crossplane control plane installation
- Declarative cloud service management
- Platform GitOps workflow

### Not Included in Baseline

- Application deployments
- Application CI/CD pipelines
- Business logic
- Runtime application operations
- Application monitoring and alerting

## Optional Services

Clark offers additional services as contract add-ons:

- **Secrets Management**: AWS Secrets Manager, Azure Key Vault, GCP Secret Manager, Vault
- **Application GitOps**: ArgoCD, Flux
- **CI/CD**: GitHub Actions, GitLab CI, Bitbucket pipelines
- **Observability**: Prometheus, Grafana, cloud-native tools
- **Security**: OPA, Kyverno, cloud-native controls

## Control Boundaries

| Area | Clark | Customer |
|------|-------|----------|
| Cloud accounts | ❌ | ✅ |
| Infrastructure code | Maintains | Owns |
| Crossplane compositions | Maintains | Owns |
| Application code | ❌ | ✅ |
| CI/CD | Optional | Owns |
| Exit capability | Always | Guaranteed |

## Why This Model Works

1. **Trust**: Customers own everything, eliminating vendor lock-in concerns
2. **Speed**: Expert team delivers infrastructure quickly
3. **Focus**: Customers focus on product, not platform
4. **Flexibility**: Optional services allow customization
5. **Exit Strategy**: Customers can always take full control

## Next Steps

- Read [Architecture](02-architecture.md) for technical details
- Review [Repository Model](03-repository-model.md) for repository structure
- Check [Responsibility Matrix](05-responsibility-matrix.md) for ownership boundaries

