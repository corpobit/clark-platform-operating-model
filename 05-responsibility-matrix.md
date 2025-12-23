# Clark Platform - Responsibility Matrix

## Overview

This document clearly defines who is responsible for what in the Clark Platform operating model. Clear boundaries prevent confusion and ensure smooth operations.

## Control Boundaries

| Area | Clark | Customer |
|------|-------|----------|
| Cloud accounts | ❌ | ✅ |
| Infrastructure code | Maintains | Owns |
| Crossplane compositions | Maintains | Owns |
| Application code | ❌ | ✅ |
| CI/CD | Optional | Owns |
| Exit capability | Always | Guaranteed |

## Detailed Responsibility Matrix

### Infrastructure Layer (clark-platform-infra)

| Responsibility | Clark | Customer | Notes |
|----------------|-------|----------|-------|
| Repository ownership | Maintainer | Owner | Customer owns, Clark maintains |
| Terraform code creation | ✅ | ❌ | Clark creates and maintains |
| Terraform code review | ✅ | ✅ | Both can review |
| Terraform state management | ✅ | ✅ | Clark manages, customer has access |
| Cloud account setup | ✅ | ✅ | Clark sets up, customer owns |
| Network provisioning | ✅ | ❌ | Clark provisions |
| Kubernetes cluster creation | ✅ | ❌ | Clark creates |
| IAM configuration | ✅ | ❌ | Clark configures |
| Monitoring setup | ✅ | ❌ | Clark sets up baseline |
| Cost optimization | ✅ | ✅ | Clark advises, customer decides |
| Security hardening | ✅ | ✅ | Clark implements, customer approves |

### Control Plane Layer (clark-platform-control)

| Responsibility | Clark | Customer | Notes |
|----------------|-------|----------|-------|
| Repository ownership | Maintainer | Owner | Customer owns, Clark maintains |
| Crossplane installation | ✅ | ❌ | Clark installs and maintains |
| Composition creation | ✅ | ❌ | Clark creates |
| Composition updates | ✅ | ✅ | Clark updates, customer can request |
| Service provisioning | ✅ | ✅ | Customer requests, Clark approves |
| Policy definition | ✅ | ✅ | Clark defines, customer approves |
| Provider configuration | ✅ | ❌ | Clark configures |
| GitOps workflow | ✅ | ✅ | Clark maintains, customer uses |
| Troubleshooting | ✅ | ✅ | Clark primary, customer assists |

### Application Layer

| Responsibility | Clark | Customer | Notes |
|----------------|-------|----------|-------|
| Application code | ❌ | ✅ | Customer owns completely |
| Application deployments | ❌ | ✅ | Customer manages |
| Application CI/CD | Optional | ✅ | Customer owns, Clark can support |
| Application monitoring | Optional | ✅ | Customer owns, Clark can support |
| Application scaling | ❌ | ✅ | Customer manages |
| Application debugging | ❌ | ✅ | Customer responsibility |

### Security and Access

| Responsibility | Clark | Customer | Notes |
|----------------|-------|----------|-------|
| Cloud account security | ✅ | ✅ | Clark configures, customer owns |
| Repository access | ✅ | ✅ | Customer controls, Clark has access |
| Kubernetes access | ✅ | ✅ | Customer controls, Clark has access |
| Secret management | Optional | ✅ | Customer owns, Clark can support |
| Compliance | ✅ | ✅ | Clark implements, customer approves |
| Security audits | ✅ | ✅ | Both participate |

### Operations

| Responsibility | Clark | Customer | Notes |
|----------------|-------|----------|-------|
| Infrastructure monitoring | ✅ | ✅ | Clark primary, customer has access |
| Incident response | ✅ | ✅ | Clark primary, customer involved |
| Change management | ✅ | ✅ | Clark reviews, customer approves |
| Documentation | ✅ | ✅ | Clark creates, customer reviews |
| Training | ✅ | ❌ | Clark provides |
| Support | ✅ | ❌ | Clark provides |

## Decision-Making Authority

### Clark Decisions

- Infrastructure architecture patterns
- Crossplane composition design
- Policy definitions
- Security configurations
- Operational procedures

### Customer Decisions

- Cloud provider selection
- Resource sizing
- Cost budgets
- Application architecture
- Deployment strategies
- Team access

### Joint Decisions

- New service additions
- Policy changes
- Architecture changes
- Security policy updates
- Major infrastructure changes

## Escalation Path

### Level 1: Standard Operations

- **Clark**: Handles routine operations
- **Customer**: Reviews and approves changes

### Level 2: Issues and Incidents

- **Clark**: Primary responder
- **Customer**: Notified and involved

### Level 3: Strategic Decisions

- **Clark**: Provides recommendations
- **Customer**: Makes final decisions

## Service Level Expectations

### Clark Commitments

- Infrastructure availability
- Response times for issues
- Change request turnaround
- Documentation updates
- Security patching

### Customer Commitments

- Timely approvals
- Access provisioning
- Resource requirements communication
- Feedback on services

## Ownership Model

### Customer Owns

- Cloud accounts
- Git repositories
- Kubernetes clusters
- Application code
- Data

### Clark Operates

- Infrastructure provisioning
- Control plane management
- GitOps workflows
- Monitoring and alerting
- Documentation

### Shared Responsibility

- Security
- Compliance
- Cost management
- Performance optimization

## Exit Strategy

### Customer Can Always

- Take full operational control
- Remove Clark access
- Clone and modify repositories
- Hire internal team
- Switch providers

### Clark Provides

- Complete documentation
- Knowledge transfer
- Access to all configurations
- Training for customer team
- Transition support

## Communication Model

### Regular Communication

- **Weekly**: Status updates
- **Monthly**: Review meetings
- **Quarterly**: Strategic planning

### Ad-Hoc Communication

- **Issues**: Immediate notification
- **Changes**: Prior notification
- **Questions**: Response within SLA

## Next Steps

- Review [Onboarding Process](06-onboarding-process.md) for initial setup
- Read [Security and Access](08-security-and-access.md) for access details
- Check [Ownership and Exit](09-ownership-and-exit.md) for exit strategy

