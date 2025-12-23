# Clark Platform - Optional Services

## Overview

Clark Platform baseline includes two core repositories. Additional services are available as contract add-ons based on customer needs.

**Why Optional Services**: Optional services are offered to adapt Clark to customer needs without enforcing tooling choices or vendor lock-in. This shows intentional design, not incompleteness. We provide flexibility while maintaining clear boundaries.

## Service Categories

### 1. Secrets Management

**Purpose**: Centralized secret storage and management

**Options**:

| Option | Description | Use Cases |
|--------|-------------|-----------|
| AWS Secrets Manager | AWS-native secret management | AWS environments |
| Azure Key Vault | Azure-native secret management | Azure environments |
| GCP Secret Manager | GCP-native secret management | GCP environments |
| HashiCorp Vault | Multi-cloud secret management | Multi-cloud, on-premises |

**What's Included**:
- Secret manager setup and configuration
- Integration with Kubernetes
- Secret rotation policies
- Access control configuration
- Documentation and training

**What's NOT Included**:
- Application secret management (customer responsibility)
- Secret creation and updates (customer responsibility)

### 2. Application GitOps

**Purpose**: GitOps tooling for application deployments

**Options**:

| Option | Description | Use Cases |
|--------|-------------|-----------|
| ArgoCD | Kubernetes-native GitOps | Kubernetes-focused teams |
| Flux | CNCF GitOps toolkit | Cloud-native workflows |

**What's Included**:
- GitOps tool installation
- Repository setup
- Workflow configuration
- Integration with platform
- Documentation and training

**What's NOT Included**:
- Application code management
- Application deployment strategies
- Application-specific configurations

### 3. CI/CD Pipelines

**Purpose**: Continuous integration and deployment pipelines

**Options**:

| Option | Description | Use Cases |
|--------|-------------|-----------|
| GitHub Actions | GitHub-native CI/CD | GitHub repositories |
| GitLab CI | GitLab-native CI/CD | GitLab repositories |
| Bitbucket Pipelines | Bitbucket-native CI/CD | Bitbucket repositories |

**What's Included**:
- Pipeline template creation
- Integration with platform
- Best practices implementation
- Documentation

**What's NOT Included**:
- Application-specific pipeline logic
- Testing strategies
- Deployment strategies

### 4. Observability

**Purpose**: Enhanced monitoring and observability

**Options**:

| Option | Description | Use Cases |
|--------|-------------|-----------|
| Prometheus | Metrics collection | Metrics-focused monitoring |
| Grafana | Visualization and dashboards | Dashboard requirements |
| Cloud-Native Tools | Provider-native tools | Provider-specific needs |

**What's Included**:
- Tool installation and configuration
- Dashboard creation
- Alerting setup
- Integration with platform
- Documentation

**What's NOT Included**:
- Application-specific metrics
- Custom application dashboards
- Application performance monitoring

### 5. Security and Compliance

**Purpose**: Enhanced security and compliance tooling

**Options**:

| Option | Description | Use Cases |
|--------|-------------|-----------|
| OPA (Open Policy Agent) | Policy enforcement | Policy-driven security |
| Kyverno | Kubernetes policy engine | Kubernetes-native policies |
| Cloud-Native Controls | Provider-native security | Provider-specific compliance |

**What's Included**:
- Policy engine installation
- Policy definition
- Integration with platform
- Compliance reporting
- Documentation

**What's NOT Included**:
- Compliance certification
- Security audits
- Application security scanning

## Service Selection Guide

### When to Choose Secrets Management

- Multiple applications need secrets
- Compliance requires centralized secret management
- Secret rotation is required
- Multi-environment secret management needed

### When to Choose Application GitOps

- Team wants GitOps for applications
- Multiple applications to manage
- Need automated deployments
- Want declarative application management

### When to Choose CI/CD Pipelines

- No existing CI/CD solution
- Want standardized pipelines
- Need platform integration
- Want best practices implementation

### When to Choose Observability

- Need advanced monitoring
- Want custom dashboards
- Need detailed metrics
- Want centralized observability

### When to Choose Security Tools

- Compliance requirements
- Need policy enforcement
- Want automated security
- Need audit capabilities

## Service Implementation

### Request Process

1. **Customer Request**
   - Identify need
   - Discuss options
   - Select service

2. **Scope Definition**
   - Define requirements
   - Estimate effort
   - Agree on timeline

3. **Contract Update**
   - Add service to contract
   - Update pricing
   - Define SLA

4. **Implementation**
   - Install and configure
   - Integrate with platform
   - Test and validate

5. **Handoff**
   - Documentation provided
   - Training conducted
   - Support established

### Timeline

- **Simple Services**: 1-2 weeks
- **Complex Services**: 2-4 weeks
- **Custom Services**: 4-8 weeks

## Service Maintenance

### Included Maintenance

- Updates and patches
- Bug fixes
- Security updates
- Documentation updates
- Basic troubleshooting

### Additional Support

- Custom configurations
- Performance tuning
- Advanced troubleshooting
- Training refreshers

## Pricing Model

### Baseline Services

- Included in base contract
- No additional cost

### Optional Services

- **One-Time Setup**: Implementation fee
- **Monthly Maintenance**: Ongoing support fee
- **Usage-Based**: For some services (e.g., secrets API calls)

## Service Combinations

### Common Combinations

- **Secrets + GitOps**: Full GitOps with secret management
- **GitOps + CI/CD**: Complete deployment pipeline
- **Observability + Security**: Comprehensive monitoring and security

### Best Practices

- Start with baseline
- Add services as needed
- Evaluate before adding
- Consider maintenance burden

## Service Retirement

### When to Retire

- Service no longer needed
- Replaced by alternative
- Cost optimization
- Simplification

### Retirement Process

1. **Notification**: Advance notice provided
2. **Migration**: Data and configs migrated
3. **Removal**: Service decommissioned
4. **Documentation**: Updated docs provided

## Future Services

### Under Consideration

- Service mesh (Istio, Linkerd)
- API gateways
- Backup and disaster recovery
- Cost optimization tools

### Request Process

- Customer requests evaluated
- Feasibility assessed
- Implementation planned
- Added to roadmap

## Next Steps

- Review [Onboarding Process](06-onboarding-process.md) for initial setup
- Check [Pricing and Engagement](10-pricing-and-engagement.md) for pricing
- Read [Responsibility Matrix](05-responsibility-matrix.md) for ownership

