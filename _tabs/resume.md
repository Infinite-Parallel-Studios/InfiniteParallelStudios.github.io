---
icon: fas fa-file-alt
order: 2
---

{% if site.portfolio.resume_pdf and site.portfolio.resume_pdf != "" %}
<a class="btn btn-primary mb-3" href="{{ site.portfolio.resume_pdf | relative_url }}" download>Download the PDF</a>
{% endif %}

**Cloud Solutions Architect | Forward Deployed AI Engineer**
Georgia, USA · Remote · [Contact me]({{ '/contact/' | relative_url }})

## Summary

Senior cloud and AI engineer with 15+ years across infrastructure, DevSecOps and multi-cloud architecture. Designs and builds agentic AI delivery systems with Claude Code and Codex, and works embedded with client teams from discovery and requirements through architecture, code, QA and production. Hands-on base in AWS (commercial and GovCloud), Terraform/Terragrunt, EKS and CI/CD, with security built in from the first commit.

## Skills

- **AI engineering:** Claude Code, Codex, agentic workflows, custom Claude skills, multi-agent orchestration, self-learning and self-healing agent loops, LLM fine-tuning, RAG, vector databases, AI code review, human-in-the-loop approval gates, least-privilege agent access
- **Forward deployed delivery:** discovery and intake, requirements, MVP scoping, statements of work (SOWs), stakeholder reporting, client sign-off, POC to production
- **Cloud and IaC:** AWS (commercial and GovCloud), Terraform/Terragrunt, EKS, Kubernetes, Docker and containers, IAM, Azure, GCP, OCI
- **CI/CD and security:** GitHub Actions, GitLab CI, secret scanning, vulnerability scanning, repository guardrails, CMMC, HIPAA, Zero Trust
- **Testing:** smoke tests, sandbox testing, web application testing, Android and iOS emulator testing
- **Languages and tools:** Python, Bash, C#, JavaScript/Node.js, n8n, Jira, Confluence, PostgreSQL, Ollama

## Professional experience

### Cloud Solutions Architect (Forward Deployed AI Engineer) · FedRock
*January 2026 – Present*

Senior engineer at a three-person cloud and AI consultancy, delivering software and cloud platforms for client companies through AI-driven workflows. Closed four client engagements since January 2026 in under four months each, work estimated at 8 to 12 months each without the AI delivery system, with ~30,000 pull requests merged across client engagements in 2026 by teams using that system.

- Designed and built 40+ custom Claude skills that run the full delivery lifecycle: discovery intake, architecture baseline, Terraform modules, Jira ticket breakdown, coding, review, QA, release, post-launch features and operations (monitoring, disaster recovery, incident response, secrets rotation, cost alerts, client handover), with human approval gates at each step.
- Forward deployed with a luxury-goods client's executive team and a 13-engineer delivery team to build a multi-tier customer platform, covering discovery, requirements, architecture, databases, application code and dev-to-production pipelines; closed about 3,500 pull requests in four months, an estimated eight months ahead of a conventional schedule.
- Set up AI pair review: Claude Code writes most of the code and Codex reviews every pull request locally against coding standards, posting findings to Jira and GitHub, with disputed findings escalated to a human architect.
- Built a merge-when-ready queue that merges pull requests one at a time once acceptance criteria, review comments and human approval are met, removing repeated re-approvals after CI across a large team.
- Built discovery skills that capture MVP scope and success metrics, then generate SOWs and metric-based stakeholder reports.
- Automated infrastructure delivery: one Terraform module per resource, dependency-ordered Jira tickets, plan and human approval before apply, drift and compliance validation, and AWS account and IAM provisioning with credentials held in a secrets vault.
- Built security and testing into the pipeline: secret and vulnerability scanning in CI, repository guardrails with CMMC and HIPAA add-on packs, and skill-driven smoke, sandbox, web and Android/iOS emulator testing.
- Built retrieval-augmented generation (RAG) systems with vector databases on self-hosted platforms, both in AWS and on local infrastructure.
- Built self-learning and self-healing AI agent loops that detect and correct their own failures and carry lessons forward into later runs, and fine-tuned existing LLMs.
- Led AWS GovCloud platform onboarding and infrastructure standardization across networking, identity, EKS and security baselines using Terraform/Terragrunt.
- Planned and executed EKS upgrades with post-change verification of clusters, nodes and add-on health.
- Stabilized GitLab CI on EKS by standardizing runner configuration templates, registration and token handling, and restart-safe behavior across runner pools.

### Cloud Solutions Architect · Transportation Security Administration (TSA) via RELI Group
*Oct 2023 – Sept 2024*

- Directed end-to-end multi-cloud modernization under strict federal compliance, improving uptime and security posture.
- Designed and deployed enterprise CI/CD pipelines and cloud-native services, reducing release time by 40%.
- Integrated Oracle SaaS with AWS services, using OIC for automation across mission-critical systems.

### Cloud Solutions Architect · Triumph Technology Solutions
*Aug 2022 – Jul 2023*

- Architected scalable multi-cloud infrastructure for enterprise clients with a focus on cost efficiency and security.
- Implemented Terraform automation across AWS, Azure and OCI, standardizing deployments enterprise-wide.
- Ran client workshops on NetSuite and Fusion SOA integrations, enabling smoother ERP adoption.

### Network Security Architect · YKK Corporation of America
*Oct 2021 – Aug 2022*

- Established security governance frameworks across multi-cloud deployments.
- Implemented enterprise-wide Terraform-driven automation for consistent, reproducible infrastructure.

Additional roles include: Senior Cloud Solutions Architect (TriFin Labs), Senior Security Manager (NCR), Senior Network Administrator (Genesis Tech), Software Architect (Enlyt Health), Lead System Architect (Atrium Health), Project Manager (A1 Power Sweepers), Software/Systems Engineer (Rockwell Automation).

## Personal projects

### Infinite Cortex · Self-hosted AI agent orchestration platform

- Built a self-hosted agent platform on a Proxmox homelab with n8n (separate dev and production), PostgreSQL, Ollama for local models, and an isolated, firewalled container for each agent.
- A Claude Code runner works Jira tickets in dependency order and opens pull requests under a GitHub App bot identity.
- Built multiple agent build-and-review loops that work tickets through to pull requests, capped at 10 rounds, with review findings saved to memory so the same mistake isn't repeated.
- Human-in-the-loop approvals gate risky changes; merged n8n workflows deploy automatically to dev, then to production after the dev check passes.
- Least-privilege by design: scoped tokens per agent, network-restricted containers and an org-wide GitHub ruleset.

[Read the Cortex case study]({% post_url 2026-10-29-infinite-cortex %})

## Past certifications

- CISSP – ISC2
- AWS Certified Solutions Architect – Professional
- Microsoft Certified: Azure Solutions Architect Expert
- Google Cloud Professional Cloud Architect
- HashiCorp Certified: Terraform Associate
- CompTIA Security+, Network+, A+
## Clearance

- Public Trust Clearance

## Education

- The Art Institutes – BFA, Computer Science
