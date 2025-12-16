# 🚀 Spacelift 
---

## 1️⃣ What is Spacelift?

**Spacelift** is a **policy‑driven Infrastructure Automation platform** used to **manage, orchestrate, and govern Infrastructure as Code (IaC)** tools like:

* Terraform
* OpenTofu
* Pulumi
* CloudFormation
* Ansible
* Kubernetes (Helm & Kustomize)

👉 Think of **Spacelift as an advanced, production‑grade replacement for Terraform Cloud + CI/CD + Governance**.

> In simple words: **Spacelift runs your IaC safely, with approvals, policies, security, and automation.**

---

## 2️⃣ Why Spacelift is Needed (Problem It Solves)

### ❌ Problems without Spacelift

* Anyone can run `terraform apply` locally
* No approval process
* No visibility of who changed infra
* No policy enforcement
* Secrets exposed in CI
* Hard to scale IaC across teams

### ✅ What Spacelift Solves

* Centralized IaC execution
* Approval-based deployments
* Policy enforcement (OPA)
* Secure secrets handling
* Audit logs
* Team collaboration

---

## 3️⃣ Where Spacelift Fits in DevOps Architecture

```
Developer → Git Push
           ↓
        Spacelift
           ↓
  Policy Checks (OPA)
           ↓
   Approval Required
           ↓
   Terraform / Ansible
           ↓
     AWS / Azure / GCP
```

---

## 4️⃣ Core Concepts of Spacelift (VERY IMPORTANT)

---

### 4.1️⃣ Stack

A **Stack** represents **one infrastructure unit**.

Examples:

* One Terraform project
* One Ansible playbook
* One Kubernetes cluster

📌 **One repo + one workflow = one stack**

#### Example

```
Repo: terraform-ec2
Stack: prod-ec2-stack
```

---

### 4.2️⃣ Worker

Workers are **execution machines** that run:

* terraform plan
* terraform apply
* ansible-playbook

Types:

* Public workers (managed by Spacelift)
* Private workers (inside your VPC)

📌 **Production always uses private workers**

---

### 4.3️⃣ Policies (OPA / Rego)

Policies are the **heart of Spacelift governance**.

They allow you to:

* Block bad infrastructure
* Enforce security rules
* Require approvals

Types of Policies:

| Policy Type     | Purpose                 |
| --------------- | ----------------------- |
| Plan Policy     | Validate terraform plan |
| Approval Policy | Require manual approval |
| Push Policy     | Control Git push        |
| Task Policy     | Control ad-hoc tasks    |
| Login Policy    | Restrict user access    |

#### Example – Block Public S3 Buckets

```rego
package spacelift

deny[msg] {
  resource := input.terraform.resource_changes[_]
  resource.type == "aws_s3_bucket"
  resource.change.after.acl == "public-read"
  msg := "Public S3 buckets are not allowed"
}
```

---

### 4.4️⃣ Contexts

**Contexts** store shared configuration:

* Environment variables
* Secrets
* Cloud credentials

📌 Reusable across multiple stacks

#### Example

```
Context: aws-prod
Variables:
  AWS_ACCESS_KEY_ID
  AWS_SECRET_ACCESS_KEY
```

---

### 4.5️⃣ Drift Detection

Spacelift **detects infrastructure drift**.

Example:

* Terraform created EC2
* Someone deletes EC2 manually from AWS Console
* Spacelift detects drift

📌 Critical for compliance & production safety

---

### 4.6️⃣ Dependencies Between Stacks

Stacks can depend on each other.

Example:

```
VPC Stack → EKS Stack → App Stack
```

Spacelift ensures correct execution order.

---

## 5️⃣ Spacelift with Terraform – Real Example

### Git Repo Structure

```
terraform-ec2/
 ├── main.tf
 ├── variables.tf
 ├── outputs.tf
```

### Workflow

1. Developer pushes code
2. Spacelift triggers plan
3. Policy validates resources
4. Approval required
5. Apply executed on worker

---

## 6️⃣ Spacelift with Ansible Example

### Use Case

* Terraform creates EC2
* Ansible configures EC2

### Flow

```
Terraform Stack → Ansible Stack
```

Spacelift manages both stacks with dependency.

---

## 7️⃣ Spacelift vs Terraform Cloud (Interview Favorite)

| Feature          | Spacelift  | Terraform Cloud  |
| ---------------- | ---------- | ---------------- |
| Multi-IaC        | ✅ Yes      | ❌ Terraform only |
| Policy Control   | ✅ Advanced | ⚠️ Limited       |
| Ansible Support  | ✅ Yes      | ❌ No             |
| Custom Workflows | ✅ Yes      | ❌ No             |
| Private Workers  | ✅ Strong   | ⚠️ Limited       |

---

## 8️⃣ Why Companies Use Spacelift

* Enterprise governance
* SOC2 / ISO compliance
* Zero trust deployments
* Multi-cloud control
* Large DevOps teams

Used by:

* FinTech
* Banking
* SaaS companies

---

## 9️⃣ Advantages of Spacelift

✅ Strong governance
✅ Policy as Code
✅ Secure secrets
✅ GitOps based
✅ Supports Terraform + Ansible + Kubernetes
✅ Scales to large teams

---

## 🔟 When NOT to Use Spacelift

❌ Small personal projects
❌ Single developer
❌ No governance needs

---

## 1️⃣1️⃣ Interview Questions (Very Important)

1. Why Spacelift over Terraform Cloud?
2. What is a stack in Spacelift?
3. How policies work in Spacelift?
4. How Spacelift handles drift?
5. Can Spacelift run Ansible?

---

## 1️⃣2️⃣ How This Helps Your 12+ LPA DevOps Goal

✔ Shows enterprise experience
✔ Governance knowledge
✔ IaC maturity
✔ Real-world DevOps tooling

---

