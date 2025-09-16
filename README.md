# AWS CI/CD Budget Monitor

A reference project that demonstrates a secure, cost-aware CI/CD pipeline on AWS with automatic budget monitoring and alerts.

## Overview
This repository provides:
- Infrastructure as Code (IaC) to provision foundational resources
- CI/CD pipeline (GitHub Actions) to build, test, and deploy
- AWS Budgets with SNS/email alerts for cost thresholds
- Guardrails and best practices to prevent runaway spend

## Architecture
- Source: GitHub repository
- CI/CD: GitHub Actions workflows (build, test, deploy)
- Deployment targets: Example AWS services (e.g., Lambda/API Gateway or ECS Fargate)
- Cost controls: AWS Budgets + SNS Topic + email subscriptions
- Observability: CloudWatch metrics/logs; optional Cost Explorer views

## Features
- Budget creation with monthly threshold and alerts at 50/80/100%
- Environment-based deployments (dev/stage/prod) with approvals
- Least-privilege IAM roles for GitHub OIDC federation
- Trunk-based workflow with PR checks and required status gates
- Automated rollback on failed deployments (example strategy)

## Getting Started
1) Fork/clone this repo.
2) Create an SNS topic and subscribe your email (or use provided IaC).
3) Configure an AWS Budget and wire alerts to the SNS topic.
4) Set up GitHub OIDC and the required AWS IAM role(s).
5) Add repository secrets (see below) and enable workflows.

## Repository Secrets
- AWS_ACCOUNT_ID: Your AWS account ID
- AWS_ROLE_TO_ASSUME: IAM role ARN for GitHub OIDC deploys
- AWS_REGION: e.g., us-east-1
- BUDGET_LIMIT: e.g., 25
- ALERT_EMAIL: destination email for budget alerts

## Workflows
- .github/workflows/ci.yml: Lint, unit tests, security scanning
- .github/workflows/deploy.yml: Build & deploy to selected environment
- .github/workflows/budget.yml: Provision/update AWS Budgets + SNS

## IaC
Examples can be provided in:
- Terraform (preferred)
- AWS CDK (TypeScript/Python)
Choose one and keep modules small and composable.

## Costs and Responsibility
You are responsible for AWS charges. Use small budgets in dev accounts and delete test resources when done.

## Roadmap
- Add sample Lambda service with CDK/Terraform
- Add Canary deployments and automated rollback
- Add cost anomaly detection integration

## Contributing
Issues and PRs are welcome. Please follow conventional commits and include tests where applicable.

## License
Choose an OSS license (MIT/Apache-2.0). Add a LICENSE file in the repo root.
