# Clark Platform - Architecture Diagrams

## System Architecture

### High-Level Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                    Customer Cloud Account                         │
│                    (Customer Owned)                              │
│                                                                   │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │         clark-platform-infra Repository                    │  │
│  │         (Customer Owned, Clark Maintained)                │  │
│  │                                                             │  │
│  │  Terraform Modules:                                         │  │
│  │  • Networking (VPC/VNet, Subnets, Routing)                │  │
│  │  • Kubernetes Clusters (EKS/GKE/AKS)                       │  │
│  │  • IAM Roles & Policies                                     │  │
│  │  • Logging & Monitoring Setup                              │  │
│  │  • Terraform State Backend                                  │  │
│  └───────────────────────┬─────────────────────────────────────┘  │
│                          │                                         │
│                          ↓ Provisions                              │
│                                                                   │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │         Kubernetes Cluster                                  │  │
│  │         (Customer Owned)                                    │  │
│  │                                                             │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │  clark-platform-control (Crossplane)               │   │  │
│  │  │  (Customer Owned, Clark Maintained)                │   │  │
│  │  │                                                      │   │  │
│  │  │  • Crossplane Core                                   │   │  │
│  │  │  • Provider Configs (AWS/GCP/Azure)                 │   │  │
│  │  │  • Compositions (Databases, Storage, Queues)        │   │  │
│  │  │  • Policies (OPA, Resource Limits)                  │   │  │
│  │  │  • GitOps Controller                                 │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  │                                                             │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │  Application Workloads                              │   │  │
│  │  │  (Customer Owned & Operated)                        │   │  │
│  │  │                                                      │   │  │
│  │  │  • Application Pods                                  │   │  │
│  │  │  • Application Services                              │   │  │
│  │  │  • Application ConfigMaps & Secrets                  │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  └───────────────────────────────────────────────────────────┘  │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

## GitOps Workflow

### Platform GitOps Flow

```
┌──────────────┐
│   Developer  │
│   Creates PR │
└──────┬───────┘
       │
       ↓
┌──────────────────────────────────┐
│  clark-platform-control          │
│  Repository (Customer Owned)      │
│  • Service Definition             │
│  • Crossplane Resource            │
└──────┬───────────────────────────┘
       │
       ↓
┌──────────────────────────────────┐
│  Clark Team Review                │
│  • Policy Compliance              │
│  • Resource Limits                │
│  • Best Practices                 │
└──────┬───────────────────────────┘
       │
       ↓
┌──────────────────────────────────┐
│  PR Merged to Main                │
└──────┬───────────────────────────┘
       │
       ↓
┌──────────────────────────────────┐
│  Crossplane Controller            │
│  • Detects Change                 │
│  • Reconciles State               │
└──────┬───────────────────────────┘
       │
       ↓
┌──────────────────────────────────┐
│  Cloud Provider API               │
│  • AWS / GCP / Azure              │
└──────┬───────────────────────────┘
       │
       ↓
┌──────────────────────────────────┐
│  Resource Provisioned             │
│  • Database / Storage / Queue     │
│  • Credentials in K8s Secrets     │
└──────────────────────────────────┘
```

## Responsibility Matrix Visual

### Ownership and Operation

```
┌─────────────────────────────────────────────────────────────┐
│                    OWNERSHIP MODEL                           │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  CUSTOMER OWNS:                    CLARK OPERATES:           │
│  ┌─────────────────────┐          ┌─────────────────────┐   │
│  │ • Cloud Accounts     │          │ • Infrastructure     │   │
│  │ • Git Repositories   │          │   Provisioning       │   │
│  │ • Kubernetes Cluster │          │ • Control Plane      │   │
│  │ • Infrastructure     │          │   Management         │   │
│  │ • Application Code   │          │ • GitOps Workflows   │   │
│  │ • Data               │          │ • Monitoring         │   │
│  └─────────────────────┘          └─────────────────────┘   │
│                                                               │
│  SHARED RESPONSIBILITY:                                       │
│  ┌─────────────────────────────────────────────────────┐     │
│  │ • Security Policies                                  │     │
│  │ • Cost Management                                    │     │
│  │ • Compliance                                         │     │
│  │ • Performance Optimization                           │     │
│  └─────────────────────────────────────────────────────┘     │
└─────────────────────────────────────────────────────────────┘
```

## Repository Structure

### Repository Relationships

```
┌─────────────────────────────────────────────────────────────┐
│                  REPOSITORY ECOSYSTEM                        │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  clark-platform-infra (Terraform)                   │    │
│  │  Owner: Customer                                     │    │
│  │  Maintainer: Clark                                   │    │
│  │                                                       │    │
│  │  Structure:                                           │    │
│  │  ├── environments/                                    │    │
│  │  │   ├── dev/                                        │    │
│  │  │   ├── staging/                                    │    │
│  │  │   └── production/                                 │    │
│  │  ├── modules/                                        │    │
│  │  │   ├── networking/                                 │    │
│  │  │   ├── kubernetes/                                │    │
│  │  │   └── iam/                                       │    │
│  │  └── terraform.tf                                   │    │
│  └─────────────────────────────────────────────────────┘    │
│                          │                                    │
│                          ↓ Provisions                         │
│                          │                                    │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  clark-platform-control (Crossplane)                │    │
│  │  Owner: Customer                                     │    │
│  │  Maintainer: Clark                                   │    │
│  │                                                       │    │
│  │  Structure:                                           │    │
│  │  ├── compositions/                                    │    │
│  │  │   ├── databases/                                  │    │
│  │  │   ├── storage/                                    │    │
│  │  │   └── queues/                                     │    │
│  │  ├── providers/                                       │    │
│  │  │   ├── aws/                                        │    │
│  │  │   ├── gcp/                                        │    │
│  │  │   └── azure/                                      │    │
│  │  ├── policies/                                        │    │
│  │  └── examples/                                        │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                               │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  Application Repositories (Optional)                 │    │
│  │  Owner: Customer                                     │    │
│  │  Managed: Customer (Clark can support)               │    │
│  │                                                       │    │
│  │  • Application Code                                   │    │
│  │  • Application GitOps (ArgoCD/Flux)                  │    │
│  │  • CI/CD Pipelines                                    │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

## Service Provisioning Flow

### End-to-End Service Request

```
┌─────────────────────────────────────────────────────────────┐
│              SERVICE PROVISIONING JOURNEY                    │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  1. DEVELOPER NEEDS SERVICE                                  │
│     ┌────────────────────┐                                   │
│     │ "I need a database"│                                   │
│     └─────────┬──────────┘                                   │
│               ↓                                               │
│  2. CREATE PR IN REPOSITORY                                  │
│     ┌─────────────────────────────────────┐                 │
│     │ apiVersion: database.example.org/v1 │                 │
│     │ kind: Database                       │                 │
│     │ metadata:                            │                 │
│     │   name: my-database                   │                 │
│     │ spec:                                │                 │
│     │   engine: postgres                    │                 │
│     │   version: "14"                       │                 │
│     └─────────┬─────────────────────────────┘                 │
│               ↓                                               │
│  3. CLARK REVIEWS PR                                          │
│     ┌─────────────────────────────────────┐                 │
│     │ ✓ Policy compliance                  │                 │
│     │ ✓ Resource limits                    │                 │
│     │ ✓ Best practices                     │                 │
│     │ ✓ Approved                           │                 │
│     └─────────┬─────────────────────────────┘                 │
│               ↓                                               │
│  4. PR MERGED                                                │
│     ┌────────────────────┐                                   │
│     │ Merge to main       │                                   │
│     └─────────┬──────────┘                                   │
│               ↓                                               │
│  5. CROSSPLANE DETECTS CHANGE                                │
│     ┌─────────────────────────────────────┐                 │
│     │ • Watches Git repository             │                 │
│     │ • Detects new resource              │                 │
│     │ • Starts reconciliation             │                 │
│     └─────────┬─────────────────────────────┘                 │
│               ↓                                               │
│  6. CLOUD PROVIDER API CALL                                  │
│     ┌─────────────────────────────────────┐                 │
│     │ • Create RDS / Cloud SQL / etc.     │                 │
│     │ • Configure networking               │                 │
│     │ • Set up security                    │                 │
│     └─────────┬─────────────────────────────┘                 │
│               ↓                                               │
│  7. RESOURCE PROVISIONED                                     │
│     ┌─────────────────────────────────────┐                 │
│     │ • Database created                   │                 │
│     │ • Credentials in K8s secrets         │                 │
│     │ • Status updated in Git              │                 │
│     │ • Ready for use                      │                 │
│     └─────────────────────────────────────┘                 │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

## Access Control Model

### Access Hierarchy

```
┌─────────────────────────────────────────────────────────────┐
│                    ACCESS CONTROL MODEL                      │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  CLOUD ACCOUNT LEVEL                                          │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Customer: Account Owner (Full Control)              │    │
│  │ Clark: IAM Role (Operational Access Only)           │    │
│  │   • Infrastructure provisioning                      │    │
│  │   • Resource management                              │    │
│  │   • Monitoring access                                │    │
│  │   • NO billing access                               │    │
│  │   • NO account deletion                              │    │
│  └─────────────────────────────────────────────────────┘    │
│                          │                                    │
│                          ↓                                    │
│  REPOSITORY LEVEL                                             │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Customer: Repository Owner (Full Control)            │    │
│  │ Clark: Maintainer (Can merge PRs, cannot delete)    │    │
│  │ Development Teams: Contributor (Can create PRs)     │    │
│  └─────────────────────────────────────────────────────┘    │
│                          │                                    │
│                          ↓                                    │
│  KUBERNETES CLUSTER LEVEL                                    │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Customer: Cluster Admin (Full Control)              │    │
│  │ Clark: Service Account (Crossplane Management Only) │    │
│  │   • crossplane-system namespace: full access        │    │
│  │   • Resource management: create/update/delete       │    │
│  │   • NO application namespace access                  │    │
│  │   • NO secret read access (except Crossplane)       │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

## Optional Services Integration

### Service Add-Ons Architecture

```
┌─────────────────────────────────────────────────────────────┐
│              OPTIONAL SERVICES INTEGRATION                   │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  BASELINE (Always Included)                                  │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ • clark-platform-infra (Terraform)                  │    │
│  │ • clark-platform-control (Crossplane)               │    │
│  │ • Basic monitoring                                   │    │
│  └─────────────────────────────────────────────────────┘    │
│                          │                                    │
│                          ↓                                    │
│  OPTIONAL SERVICES (Add-Ons)                                 │
│  ┌─────────────────────────────────────────────────────┐    │
│  │                                                     │    │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────┐ │    │
│  │  │   Secrets    │  │  App GitOps  │  │   CI/CD   │ │    │
│  │  │  Management  │  │  (ArgoCD/    │  │  Pipelines│ │    │
│  │  │              │  │   Flux)      │  │           │ │    │
│  │  └──────────────┘  └──────────────┘  └──────────┘ │    │
│  │                                                     │    │
│  │  ┌──────────────┐  ┌──────────────┐               │    │
│  │  │Observability │  │   Security   │               │    │
│  │  │(Prometheus/  │  │   (OPA/      │               │    │
│  │  │  Grafana)    │  │   Kyverno)   │               │    │
│  │  └──────────────┘  └──────────────┘               │    │
│  │                                                     │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

## Onboarding Timeline

### 4-Week Onboarding Process

```
┌─────────────────────────────────────────────────────────────┐
│                    ONBOARDING TIMELINE                       │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  WEEK 1: SETUP & PREPARATION                                 │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ • Cloud account setup                                │    │
│  │ • Repository cloning                                 │    │
│  │ • Requirements gathering                             │    │
│  │ • Initial configuration                              │    │
│  └─────────────────────────────────────────────────────┘    │
│                          │                                    │
│                          ↓                                    │
│  WEEK 2-3: INFRASTRUCTURE PROVISIONING                       │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ • Network infrastructure (VPC/VNet)                 │    │
│  │ • Kubernetes cluster creation                       │    │
│  │ • IAM and security setup                            │    │
│  │ • Monitoring baseline                                │    │
│  └─────────────────────────────────────────────────────┘    │
│                          │                                    │
│                          ↓                                    │
│  WEEK 3-4: CONTROL PLANE & TRAINING                          │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ • Crossplane installation                           │    │
│  │ • GitOps workflow setup                             │    │
│  │ • First service provisioning                         │    │
│  │ • Team training                                     │    │
│  └─────────────────────────────────────────────────────┘    │
│                          │                                    │
│                          ↓                                    │
│  WEEK 5-8: STABILIZATION                                     │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ • Monitoring and optimization                        │    │
│  │ • Issue resolution                                  │    │
│  │ • Process refinement                                │    │
│  │ • Ongoing support                                   │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

## Exit Process Flow

### Customer Exit Journey

```
┌─────────────────────────────────────────────────────────────┐
│                      EXIT PROCESS                            │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  1. NOTIFICATION                                              │
│     ┌────────────────────┐                                   │
│     │ Customer notifies │                                   │
│     │ Clark of exit     │                                   │
│     └─────────┬──────────┘                                   │
│               ↓                                               │
│  2. KNOWLEDGE TRANSFER                                        │
│     ┌─────────────────────────────────────┐                 │
│     │ • Documentation review              │                 │
│     │ • Training sessions                 │                 │
│     │ • Handover meetings                 │                 │
│     │ • Q&A sessions                      │                 │
│     └─────────┬─────────────────────────────┘                 │
│               ↓                                               │
│  3. ACCESS TRANSFER                                           │
│     ┌─────────────────────────────────────┐                 │
│     │ • Customer already has full access  │                 │
│     │ • Transfer operational access       │                 │
│     │ • Credential handover               │                 │
│     │ • Access verification               │                 │
│     └─────────┬─────────────────────────────┘                 │
│               ↓                                               │
│  4. CODE & CONFIG TRANSFER                                    │
│     ┌─────────────────────────────────────┐                 │
│     │ • Repository access (already owned) │                 │
│     │ • Configuration export               │                 │
│     │ • State transfer                     │                 │
│     │ • Complete documentation package      │                 │
│     └─────────┬─────────────────────────────┘                 │
│               ↓                                               │
│  5. SUPPORT TRANSITION                                        │
│     ┌─────────────────────────────────────┐                 │
│     │ • Optional transition period        │                 │
│     │ • Support handoff                    │                 │
│     │ • Final review and sign-off         │                 │
│     └─────────────────────────────────────┘                 │
│                                                               │
│  TIMELINE: 2-4 weeks standard                                │
│  NO PENALTIES: Exit anytime, no lock-in                      │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

