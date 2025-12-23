# Clark Platform - Repository Model

## Overview

Each customer receives two core repositories that form the foundation of their platform infrastructure. These repositories are cloned from Clark templates and fully owned by the customer.

## Core Repositories

### 1. clark-platform-infra

**Purpose**: Foundational infrastructure via Terraform

**Ownership**: Customer (operated by Clark)

**Contents**:
- Terraform modules for cloud infrastructure
- Network configurations (VPC/VNet, subnets, routing)
- Kubernetes cluster definitions
- IAM roles and policies
- Logging and monitoring setup
- Terraform state backend configuration

**Structure**:
```
clark-platform-infra/
├── environments/
│   ├── dev/
│   ├── staging/
│   └── production/
├── modules/
│   ├── networking/
│   ├── kubernetes/
│   └── iam/
├── terraform.tf
└── README.md
```

**Access**:
- Customer: Full owner access
- Clark: Maintainer access for operations

**What It Manages**:
- Cloud accounts and subscriptions
- Networking infrastructure
- Kubernetes clusters
- IAM and access boundaries
- Logging and monitoring baselines
- Terraform state and backend

**What It Does NOT Manage**:
- Application deployments
- Application configurations
- Business logic
- Runtime operations

### 2. clark-platform-control

**Purpose**: Cloud service control plane via Crossplane

**Ownership**: Customer (operated by Clark)

**Contents**:
- Crossplane compositions
- Cloud service definitions
- Provider configurations
- Policy definitions
- GitOps configurations

**Structure**:
```
clark-platform-control/
├── compositions/
│   ├── databases/
│   ├── storage/
│   └── queues/
├── providers/
│   ├── aws/
│   ├── gcp/
│   └── azure/
├── policies/
├── examples/
└── README.md
```

**Access**:
- Customer: Full owner access
- Clark: Maintainer access for operations
- Development teams: Contributor access

**What It Manages**:
- Declarative cloud services
- Databases, storage, queues
- Managed Kubernetes addons
- Provider abstraction (AWS/GCP/Azure)
- Policy and guardrails
- Platform GitOps

**What It Does NOT Manage**:
- Application code
- Application deployments
- Application CI/CD

## Repository Lifecycle

### Initial Setup

1. **Template Cloning**: Clark clones templates for customer
2. **Customization**: Customer-specific configurations applied
3. **Access Setup**: Customer becomes owner, Clark becomes maintainer
4. **Initial Provisioning**: Clark provisions initial infrastructure

### Ongoing Operations

1. **Change Requests**: Developers create PRs
2. **Clark Review**: Clark team reviews and approves
3. **Automation**: Changes applied via GitOps
4. **Monitoring**: Clark monitors infrastructure health

### Ownership Transfer

1. **Documentation**: All configurations documented
2. **Knowledge Transfer**: Clark provides training
3. **Access Transfer**: Customer gains full operational access
4. **Support Transition**: Optional ongoing support available

## Repository Relationships

```
┌─────────────────────────────────────────┐
│   clark-platform-infra (Terraform)      │
│   • Provisions foundational infra       │
│   • Creates Kubernetes cluster          │
└──────────────┬──────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────┐
│   Kubernetes Cluster (Customer Owned)   │
│                                          │
│   ┌──────────────────────────────────┐  │
│   │ clark-platform-control           │  │
│   │ (Crossplane)                     │  │
│   │ • Manages cloud services         │  │
│   │ • Installed on cluster           │  │
│   └──────────────────────────────────┘  │
│                                          │
│   ┌──────────────────────────────────┐  │
│   │ Application Workloads             │  │
│   │ (Customer Owned)                  │  │
│   └──────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

## Optional Repositories

### DevOps Pipeline Repository

**Status**: Not included in baseline

**Rationale**:
- Pipelines are highly opinionated
- High maintenance burden
- Customers often have existing tooling
- Scope creep concern

**Future Consideration**:
- Phase 1 (MVP): Reference pipelines in documentation
- Phase 2 (Early customers): Clone on-demand if requested
- Phase 3 (Later): Optional template repository

### Application GitOps Repository

**Status**: Optional service

**Options**:
- ArgoCD
- Flux

**Ownership**: Customer (Clark can provide support)

## Access Control Model

### Repository Access Levels

| Role | clark-platform-infra | clark-platform-control |
|------|----------------------|------------------------|
| Customer | Owner | Owner |
| Clark | Maintainer | Maintainer |
| Development Teams | Read (optional) | Contributor |

### Access Principles

- **Customer Ownership**: Customer always has owner access
- **Clark Operations**: Clark has maintainer access for operations
- **Team Access**: Development teams have appropriate access levels
- **Audit Trail**: All changes tracked in Git history

## Version Control

### Branching Strategy

- **Main Branch**: Production-ready configurations
- **Feature Branches**: New infrastructure or services
- **Environment Branches**: Separate branches per environment (optional)

### Change Management

1. **Pull Requests**: All changes via PR
2. **Review Process**: Clark reviews infrastructure changes
3. **Testing**: Changes tested in development first
4. **Deployment**: Automated via GitOps or Terraform

## Documentation

### Repository Documentation

Each repository includes:
- README.md with overview and setup instructions
- Architecture documentation
- Examples and templates
- Change management process

### External Documentation

- This operating model repository
- Customer-specific runbooks
- Incident response procedures

## Best Practices

### Repository Management

- Keep repositories focused on their purpose
- Document all configurations
- Use version tags for releases
- Maintain clear commit messages

### Change Management

- Small, incremental changes
- Review before merge
- Test in development first
- Document breaking changes

### Security

- No secrets in repositories
- Use secret management systems
- Regular security audits
- Access reviews

## Next Steps

- Read [GitOps Model](04-gitops-model.md) for workflow details
- Review [Responsibility Matrix](05-responsibility-matrix.md) for ownership
- Check [Security and Access](08-security-and-access.md) for access control

