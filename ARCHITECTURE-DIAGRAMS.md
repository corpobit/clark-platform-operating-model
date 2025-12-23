# Clark Platform - Architecture Diagrams

## System Architecture

### High-Level Overview

```mermaid
flowchart TB
    subgraph CloudAccount["Customer Cloud Account (Customer Owned)"]
        subgraph InfraRepo["clark-platform-infra Repository<br/>(Customer Owned, Clark Maintained)"]
            Terraform["Terraform Modules<br/>• Networking (VPC/VNet, Subnets, Routing)<br/>• Kubernetes Clusters (EKS/GKE/AKS)<br/>• IAM Roles & Policies<br/>• Logging & Monitoring Setup<br/>• Terraform State Backend"]
        end
        
        subgraph K8sCluster["Kubernetes Cluster (Customer Owned)"]
            subgraph ControlPlane["clark-platform-control (Crossplane)<br/>(Customer Owned, Clark Maintained)"]
                Crossplane["• Crossplane Core<br/>• Provider Configs (AWS/GCP/Azure)<br/>• Compositions (Databases, Storage, Queues)<br/>• Policies (OPA, Resource Limits)<br/>• GitOps Controller"]
            end
            
            subgraph Apps["Application Workloads<br/>(Customer Owned & Operated)"]
                AppWorkloads["• Application Pods<br/>• Application Services<br/>• Application ConfigMaps & Secrets"]
            end
        end
    end
    
    Terraform -->|Provisions| K8sCluster
```

## GitOps Workflow

### Platform GitOps Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Dashboard as Clark Dashboard
    participant Clark as Clark Team
    participant Repo as clark-platform-control<br/>Repository<br/>(Customer Owned)
    participant XP as Crossplane Controller
    participant Cloud as Cloud Provider API<br/>(AWS/GCP/Azure)
    participant Resource as Resource Provisioned
    
    Dev->>Dashboard: Request Resource/Service<br/>Report Incident<br/>Create Case
    Dashboard->>Clark: Review Request
    Clark->>Clark: Policy Compliance<br/>Resource Limits<br/>Best Practices
    Clark->>Repo: Creates PR<br/>(Service Definition,<br/>Crossplane Resource)
    Clark->>Repo: Approve & Merge
    Repo->>XP: Detects Change
    XP->>XP: Reconciles State
    XP->>Cloud: API Call
    Cloud->>Resource: Provision Resource<br/>(Database/Storage/Queue)
    Resource->>Resource: Credentials in K8s Secrets
    Resource->>Dashboard: Status Update
    Dashboard->>Dev: Notification
```

## Responsibility Matrix Visual

### Ownership and Operation

```mermaid
flowchart LR
    subgraph Customer["CUSTOMER OWNS"]
        CA[Cloud Accounts]
        GR[Git Repositories]
        KC[Kubernetes Cluster]
        INF[Infrastructure]
        AC[Application Code]
        DATA[Data]
    end
    
    subgraph Clark["CLARK OPERATES"]
        IP[Infrastructure<br/>Provisioning]
        CP[Control Plane<br/>Management]
        GW[GitOps Workflows]
        MON[Monitoring]
    end
    
    subgraph Shared["SHARED RESPONSIBILITY"]
        SP[Security Policies]
        CM[Cost Management]
        COMP[Compliance]
        PO[Performance<br/>Optimization]
    end
```

## Repository Structure

### Repository Relationships

```mermaid
flowchart TB
    subgraph RepoEco["REPOSITORY ECOSYSTEM"]
        subgraph InfraRepo["clark-platform-infra (Terraform)<br/>Owner: Customer | Maintainer: Clark"]
            InfraStruct["Structure:<br/>├── environments/<br/>│   ├── dev/<br/>│   ├── staging/<br/>│   └── production/<br/>├── modules/<br/>│   ├── networking/<br/>│   ├── kubernetes/<br/>│   └── iam/<br/>└── terraform.tf"]
        end
        
        subgraph ControlRepo["clark-platform-control (Crossplane)<br/>Owner: Customer | Maintainer: Clark"]
            ControlStruct["Structure:<br/>├── compositions/<br/>│   ├── databases/<br/>│   ├── storage/<br/>│   └── queues/<br/>├── providers/<br/>│   ├── aws/<br/>│   ├── gcp/<br/>│   └── azure/<br/>├── policies/<br/>└── examples/"]
        end
        
        subgraph AppRepo["Application Repositories (Optional)<br/>Owner: Customer | Managed: Customer<br/>(Clark can support)"]
            AppStruct["• Application Code<br/>• Application GitOps (ArgoCD/Flux)<br/>• CI/CD Pipelines"]
        end
    end
    
    InfraRepo -->|Provisions| ControlRepo
```

## Service Provisioning Flow

### End-to-End Service Request

```mermaid
flowchart TD
    Start([Developer Needs Service<br/>I need a database]) --> Request[Request via Clark Dashboard<br/>Fill in details:<br/>engine: postgres, version: 14]
    Request --> Review[Clark Reviews Request<br/>✓ Policy compliance<br/>✓ Resource limits<br/>✓ Best practices<br/>✓ Approved]
    Review --> CreatePR[Clark Creates PR in Repository<br/>apiVersion: database.example.org/v1<br/>kind: Database<br/>spec: engine: postgres, version: 14]
    CreatePR --> Merge[Clark Merges PR to Main]
    Merge --> Detect[Crossplane Detects Change<br/>• Watches Git repository<br/>• Detects new resource<br/>• Starts reconciliation]
    Detect --> API[Cloud Provider API Call<br/>• Create RDS / Cloud SQL / etc.<br/>• Configure networking<br/>• Set up security]
    API --> Provisioned[Resource Provisioned<br/>• Database created<br/>• Credentials in K8s secrets<br/>• Status updated in Git & Dashboard<br/>• Developer notified]
```

## Access Control Model

### Access Hierarchy

```mermaid
flowchart TD
    subgraph CloudLevel["CLOUD ACCOUNT LEVEL"]
        CloudCust[Customer: Account Owner<br/>Full Control]
        CloudClark[Clark: IAM Role<br/>Operational Access Only<br/>• Infrastructure provisioning<br/>• Resource management<br/>• Monitoring access<br/>• NO billing access<br/>• NO account deletion]
    end
    
    subgraph RepoLevel["REPOSITORY LEVEL"]
        RepoCust[Customer: Repository Owner<br/>Full Control]
        RepoClark[Clark: Maintainer<br/>Can merge PRs, cannot delete]
        RepoDev[Development Teams: Contributor<br/>Can create issues in repo]
    end
    
    subgraph K8sLevel["KUBERNETES CLUSTER LEVEL"]
        K8sCust[Customer: Cluster Admin<br/>Full Control]
        K8sClark[Clark: Service Account<br/>Crossplane Management Only<br/>• crossplane-system namespace: full access<br/>• Resource management: create/update/delete<br/>• NO application namespace access<br/>• NO secret read access (except Crossplane)]
    end
    
    CloudLevel --> RepoLevel
    RepoLevel --> K8sLevel
```

## Optional Services Integration

### Service Add-Ons Architecture

```mermaid
flowchart TB
    subgraph Baseline["BASELINE (Always Included)"]
        Infra[clark-platform-infra<br/>(Terraform)]
        Control[clark-platform-control<br/>(Crossplane)]
        Monitor[Basic monitoring]
    end
    
    subgraph Optional["OPTIONAL SERVICES (Add-Ons)"]
        Secrets[Secrets Management<br/>AWS Secrets Manager<br/>Azure Key Vault<br/>Vault]
        GitOps[App GitOps<br/>ArgoCD / Flux]
        CICD[CI/CD Pipelines<br/>GitHub Actions<br/>GitLab CI]
        Observability[Observability<br/>Prometheus / Grafana]
        Security[Security<br/>OPA / Kyverno]
    end
    
    Baseline --> Optional
```

## Onboarding Timeline

### 4-Week Onboarding Process

```mermaid
gantt
    title Onboarding Timeline
    dateFormat YYYY-MM-DD
    section Week 1
    Cloud account setup           :2024-01-01, 7d
    Repository cloning            :2024-01-01, 7d
    Requirements gathering        :2024-01-01, 7d
    Initial configuration         :2024-01-01, 7d
    
    section Week 2-3
    Network infrastructure        :2024-01-08, 14d
    Kubernetes cluster creation   :2024-01-08, 14d
    IAM and security setup        :2024-01-08, 14d
    Monitoring baseline           :2024-01-08, 14d
    
    section Week 3-4
    Crossplane installation       :2024-01-22, 7d
    GitOps workflow setup         :2024-01-22, 7d
    First service provisioning    :2024-01-22, 7d
    Team training                 :2024-01-22, 7d
    
    section Week 5-8
    Monitoring and optimization   :2024-01-29, 28d
    Issue resolution              :2024-01-29, 28d
    Process refinement            :2024-01-29, 28d
    Ongoing support              :2024-01-29, 28d
```

## Exit Process Flow

### Customer Exit Journey

```mermaid
flowchart TD
    Start([Customer Notifies<br/>Clark of Exit]) --> Knowledge[Knowledge Transfer<br/>• Documentation review<br/>• Training sessions<br/>• Handover meetings<br/>• Q&A sessions]
    Knowledge --> Access[Access Transfer<br/>• Customer already has full access<br/>• Transfer operational access<br/>• Credential handover<br/>• Access verification]
    Access --> Code[Code & Config Transfer<br/>• Repository access (already owned)<br/>• Configuration export<br/>• State transfer<br/>• Complete documentation package]
    Code --> Support[Support Transition<br/>• Optional transition period<br/>• Support handoff<br/>• Final review and sign-off]
    Support --> End([Exit Complete])
    
    style Start fill:#e1f5ff
    style End fill:#d4edda
```

