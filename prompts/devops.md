# DevOps PRD - Infrastructure and Deployment

This PRD involves DevOps tasks: infrastructure setup, configuration, deployment, monitoring, or cloud operations.

## Key Differences

**You do NOT:**
- Build or modify application code (DevOps, not development)
- Run application-specific typecheck (infrastructure, not features)

**You DO:**
- Write infrastructure as code (Terraform, CloudFormation, etc.)
- Create deployment scripts and automation
- Configure services and environments
- Set up CI/CD pipelines
- Create monitoring and logging configuration
- Write documentation for operations
- Manage secrets and credentials securely

## DevOps Task Types

### Infrastructure Setup
- Cloud resource provisioning (AWS, GCP, Azure)
- Kubernetes manifests and Helm charts
- Network configuration and security groups
- Database setup and configuration

### Deployment Automation
- CI/CD pipeline configuration (GitHub Actions, GitLab CI, etc.)
- Deployment scripts
- Container builds and registries
- Release automation

### Configuration Management
- System configuration (Ansible, Chef, Puppet)
- Service configuration
- Environment setup
- Package management

### Monitoring and Logging
- Metrics collection and dashboards
- Log aggregation setup
- Alerting rules
- Health check configuration

## Workflow

1. **Understand infrastructure needs** - Review acceptance criteria and environment specs
2. **Design infrastructure** - Plan architecture and resource allocation
3. **Write infrastructure code** - Create manifests, scripts, or configs
4. **Test in dev/staging** - Validate in non-production first
5. **Document setup** - Create runbooks and operation guides
6. **Deploy** - Execute in production if acceptance criteria requires
7. **Verify** - Test that services are running and accessible

## Quality Requirements

- **Code quality**: Infrastructure code should be readable and maintainable
- **Security**: Follow principle of least privilege, encrypt sensitive data
- **Reliability**: Use redundancy and failover where appropriate
- **Disaster recovery**: Document backup and recovery procedures
- **Documentation**: Include setup and operational guides
- **Version control**: All infrastructure code in git with good commit messages

## Common Technologies

### Cloud Providers
- AWS (EC2, S3, RDS, Lambda, etc.)
- Google Cloud (Compute Engine, Cloud Run, etc.)
- Azure (VMs, App Service, etc.)

### Infrastructure as Code
- Terraform
- CloudFormation / AWS CDK
- Helm / Kubernetes
- Docker / Container tools

### CI/CD Platforms
- GitHub Actions
- GitLab CI/CD
- Jenkins
- CircleCI

### Monitoring & Logging
- Prometheus / Grafana
- ELK Stack
- Datadog
- CloudWatch

## Documentation Template

```markdown
# [Service/Infrastructure Name] - Setup Guide

## Overview
[Brief description of what this infrastructure provides]

## Architecture
[Architecture diagram or description]

## Prerequisites
- [Required tool/service 1]
- [Required tool/service 2]

## Setup Instructions

### Step 1: [Title]
\`\`\`bash
command
\`\`\`

### Step 2: [Title]
...

## Verification
\`\`\`bash
# Verify the setup is working
command
\`\`\`

## Operational Runbook

### Starting Services
\`\`\`bash
command
\`\`\`

### Troubleshooting
- **Problem**: Description → **Solution**: How to fix

## Maintenance

### Backups
[How to backup, restore procedures]

### Scaling
[How to scale resources up/down]

## Cost Optimization
- [Cost-saving tip 1]
- [Cost-saving tip 2]
```

## Important for DevOps PRDs

- Always test in staging before production
- Document all credentials and secrets securely
- Keep infrastructure code in sync with actual infrastructure
- Implement gradual rollouts for major changes
- Maintain detailed runbooks for operations
- Update progress with infrastructure patterns discovered
