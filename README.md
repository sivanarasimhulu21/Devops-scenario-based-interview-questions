
# DevOps Scenario-Based Interview Questions

A growing, practical knowledge base of real-world DevOps, SRE, Cloud, Linux, CI/CD, infrastructure, monitoring, and production troubleshooting scenarios.

This repository documents how to investigate problems, identify root causes, apply fixes, and explain solutions in technical interviews.

## Objectives

- Practice real-world DevOps and SRE troubleshooting.
- Prepare for scenario-based technical interviews.
- Maintain practical Linux and cloud troubleshooting commands.
- Document root causes, solutions, and preventive measures.
- Build a searchable, long-term technical knowledge base.

## Technology Coverage

Linux | AWS | Docker | Kubernetes | Jenkins | CI/CD | Git | Maven | Terraform | Ansible | Prometheus | Grafana | Networking | Security | Production Support

## Scenario Index

Each scenario has a unique ID and its own Markdown file.

### 01. Linux Administration

| ID | Scenario | File |
|---|---|---|
| SCN-001 | Linux disk usage reaches 100% | [Read scenario](01-linux/SCN-001-disk-usage-100-percent.md) |
| SCN-002 | Linux server has high CPU usage | [Read scenario](01-linux/SCN-002-high-cpu-usage.md) |
| SCN-003 | Linux server fails to boot | [Read scenario](01-linux/SCN-003-linux-server-not-booting.md) |

### 02. AWS and Cloud

| ID | Scenario | File |
|---|---|---|
| SCN-004 | EC2 instance is unreachable | [Read scenario](02-aws-cloud/SCN-004-ec2-instance-unreachable.md) |

### 03. Docker and Containers

| ID | Scenario | File |
|---|---|---|
| SCN-005 | Docker container keeps restarting | [Read scenario](03-docker-containers/SCN-005-container-keeps-restarting.md) |

### 04. Jenkins and CI/CD

| ID | Scenario | File |
|---|---|---|
| SCN-006 | Jenkins pipeline fails | [Read scenario](04-cicd-jenkins/SCN-006-jenkins-pipeline-failed.md) |

### 05. Kubernetes

| ID | Scenario | File |
|---|---|---|
| SCN-007 | Kubernetes pod enters CrashLoopBackOff | [Read scenario](05-kubernetes/SCN-007-pod-crashloopbackoff.md) |

### 06. Terraform and Ansible

Add infrastructure provisioning and configuration management scenarios here.

### 07. Monitoring and Observability

Add Prometheus, Grafana, alerting, logging, and incident detection scenarios here.

### 08. Networking and Security

Add DNS, ports, routing, firewalls, TLS, IAM, and access-control scenarios here.

### 09. Git, Maven and Artifacts

Add Git conflicts, build failures, dependency problems, and artifact repository scenarios here.

### 10. Production Incidents

Add outages, failed deployments, service degradation, rollback, and recovery scenarios here.

---

## File Naming Convention

Use this format for every new scenario:

`SCN-NNN-short-descriptive-title.md`

Examples:

- `SCN-008-terraform-apply-failed.md`
- `SCN-009-prometheus-target-down.md`
- `SCN-010-nginx-502-bad-gateway.md`

Rules:

1. Assign the next unused global scenario ID.
2. Use lowercase filenames with hyphens.
3. Keep one main problem in each file.
4. Place the file in the appropriate category folder.
5. Add a link and short description to this README.
6. Never reuse an existing scenario ID.

## Standard Scenario Format

Every scenario should contain:

1. Scenario title and ID
2. Problem statement
3. Environment and symptoms
4. Possible causes
5. Investigation steps and commands
6. Root cause
7. Solution and verification
8. Prevention and best practices
9. Interview-ready explanation
10. References, if applicable

## How to Use This Repository

- Choose a scenario and understand the symptoms.
- Try troubleshooting before reading the solution.
- Execute commands in a safe lab environment.
- Record what you observed and what fixed the problem.
- Explain the root cause in your own words.
- Update the index whenever you add a scenario.

## Contribution and Maintenance

This repository is maintained as a continuously growing personal learning resource.

New scenarios may be added as new technologies, incidents, interview questions, and lessons are encountered.

**Goal:** Learn the problem, investigate the evidence, fix the issue, verify the result, and prevent recurrence.

---

Maintained by [Siva Narasimhulu](https://github.com/Sivanarasimhulu21)
