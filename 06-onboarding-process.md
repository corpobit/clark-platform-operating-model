# Clark Platform - Onboarding Process

## Overview

This document outlines the step-by-step process for onboarding a new customer to the Clark Platform.

## Pre-Onboarding

### Discovery Phase

1. **Initial Consultation**
   - Understand customer requirements
   - Assess cloud provider needs
   - Identify optional services
   - Discuss timeline and budget

2. **Proposal**
   - Scope of work defined
   - Pricing and engagement model
   - Timeline and milestones
   - Success criteria

3. **Contract Signing**
   - Service agreement
   - SLA definitions
   - Access requirements
   - Payment terms

## Onboarding Phases

### Phase 1: Setup and Preparation (Week 1)

#### 1.1 Account Setup

- **Cloud Account Creation**
  - Customer creates cloud account
  - Clark receives operational access
  - IAM roles configured
  - Billing setup

- **Repository Setup**
  - Clone `clark-platform-infra` template
  - Clone `clark-platform-control` template
  - Customer becomes repository owner
  - Clark becomes maintainer
  - Access permissions configured

#### 1.2 Initial Configuration

- **Customer Requirements Gathering**
  - Environment definitions (dev/staging/prod)
  - Resource requirements
  - Network topology preferences
  - Security requirements
  - Compliance needs

- **Configuration Customization**
  - Terraform variables configured
  - Crossplane compositions customized
  - Policies defined
  - Naming conventions established

### Phase 2: Infrastructure Provisioning (Week 2-3)

#### 2.1 Network Infrastructure

- **VPC/VNet Creation**
  - Network topology designed
  - Subnets configured
  - Routing tables set up
  - NAT gateways provisioned
  - Security groups configured

#### 2.2 Kubernetes Cluster

- **Cluster Provisioning**
  - Cluster created via Terraform
  - Node groups configured
  - Networking configured
  - IAM roles assigned
  - Cluster access configured

#### 2.3 Baseline Services

- **Monitoring Setup**
  - Cloud provider monitoring enabled
  - Logging configured
  - Alerting rules defined
  - Dashboard access provided

- **Security Baseline**
  - IAM policies applied
  - Network policies configured
  - Encryption enabled
  - Access controls set

### Phase 3: Control Plane Installation (Week 3-4)

#### 3.1 Crossplane Installation

- **Crossplane Deployment**
  - Crossplane installed on cluster
  - Providers configured (AWS/GCP/Azure)
  - Compositions deployed
  - Policies applied

#### 3.2 GitOps Setup

- **GitOps Workflow**
  - GitOps controller configured
  - Repository sync configured
  - Access controls set
  - Workflow documented

#### 3.3 Initial Services

- **First Service Provisioning**
  - Example service provisioned
  - Workflow demonstrated
  - Documentation provided
  - Team training initiated

### Phase 4: Training and Handoff (Week 4)

#### 4.1 Team Training

- **Platform Overview**
  - Architecture explained
  - Repository structure
  - GitOps workflow
  - Service provisioning process

- **Hands-On Training**
  - Creating service requests
  - Reviewing changes
  - Troubleshooting basics
  - Best practices

#### 4.2 Documentation

- **Customer-Specific Docs**
  - Architecture diagrams
  - Runbooks
  - Troubleshooting guides
  - Contact information

#### 4.3 Access Provisioning

- **Team Access**
  - Developer access to repositories
  - Kubernetes cluster access
  - Monitoring dashboard access
  - Support channel access

## Post-Onboarding

### Week 5-8: Stabilization

- **Monitoring**
  - Infrastructure health
  - Service usage
  - Performance metrics
  - Cost tracking

- **Support**
  - Issue resolution
  - Questions answered
  - Workflow refinements
  - Documentation updates

### Ongoing Operations

- **Regular Reviews**
  - Weekly status updates
  - Monthly review meetings
  - Quarterly planning

- **Continuous Improvement**
  - Process improvements
  - Tool enhancements
  - Best practice updates
  - Training refreshers

## Onboarding Checklist

### Customer Responsibilities

- [ ] Cloud account created
- [ ] Billing configured
- [ ] Initial requirements provided
- [ ] Team members identified
- [ ] Access credentials provided
- [ ] Training sessions attended
- [ ] Documentation reviewed

### Clark Responsibilities

- [ ] Repositories cloned and configured
- [ ] Infrastructure provisioned
- [ ] Control plane installed
- [ ] GitOps workflow configured
- [ ] Documentation created
- [ ] Training provided
- [ ] Access configured
- [ ] Initial services provisioned

## Timeline

### Standard Onboarding

- **Week 1**: Setup and preparation
- **Week 2-3**: Infrastructure provisioning
- **Week 3-4**: Control plane installation
- **Week 4**: Training and handoff
- **Week 5-8**: Stabilization

### Accelerated Onboarding

- **Week 1**: Setup and infrastructure
- **Week 2**: Control plane and training
- **Week 3**: Stabilization

*Note: Accelerated onboarding requires dedicated resources and may have additional costs.*

## Success Criteria

### Technical Success

- [ ] Infrastructure provisioned and healthy
- [ ] Control plane operational
- [ ] GitOps workflow functional
- [ ] First service successfully provisioned
- [ ] Monitoring and alerting working

### Operational Success

- [ ] Team trained and comfortable
- [ ] Documentation complete
- [ ] Support channels established
- [ ] Processes understood
- [ ] Access properly configured

### Business Success

- [ ] Customer satisfied with setup
- [ ] Clear path forward established
- [ ] Support model understood
- [ ] Expectations aligned
- [ ] Relationship established

## Common Challenges

### Challenge: Cloud Account Delays

**Solution**: Start with repository setup and documentation while waiting

### Challenge: Complex Requirements

**Solution**: Phased approach, start simple, iterate

### Challenge: Team Availability

**Solution**: Flexible training schedule, recorded sessions

### Challenge: Access Issues

**Solution**: Clear access requirements upfront, test early

## Next Steps

After onboarding:

- Review [Optional Services](07-optional-services.md) for add-ons
- Check [Security and Access](08-security-and-access.md) for access management
- Read [Pricing and Engagement](10-pricing-and-engagement.md) for ongoing model

