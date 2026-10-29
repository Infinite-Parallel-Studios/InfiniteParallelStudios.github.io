---
icon: fas fa-diagram-project
order: 1
---

Each project gets a write-up in the shape I'd use to walk an engineering team through it: the problem, the architecture, the decisions and trade-offs, how it fails, and what I learned. Where a project can be shown, it has a demo.

## Infinite Cortex

*Personal project · Self-hosted AI agent orchestration platform*

A self-hosted platform where a Claude Code runner takes Jira tickets in dependency order, opens pull requests under a GitHub App bot identity, and a Codex reviewer in its own container reviews each one before a human merges. Workflows ship automatically from dev to production after a dev check, and risky changes wait on a human approval.

**Stack:** Claude Code, Codex, n8n, Jira, GitHub Apps, PostgreSQL, Ollama, Proxmox containers

{% include demo.html video="" caption="Infinite Cortex: one ticket from Jira to a reviewed, merged pull request" %}

[Read the case study]({% post_url 2026-10-29-infinite-cortex %})

## AI delivery system for client engagements

*Client work at FedRock · Clients named by industry only*

An AI-driven delivery workflow built from 40+ custom Claude skills that run the full lifecycle, from discovery intake and SOWs through architecture, Terraform, Jira ticket breakdown, coding, review, QA, release and operations, with human approval gates at each step. Claude Code writes most of the code, Codex reviews every pull request against coding standards, and a merge-when-ready queue merges pull requests one at a time once acceptance criteria, review comments and human approval are met.

Teams using the system merged ~30,000 pull requests across client engagements in 2026. On one engagement, forward deployed with a luxury-goods client's executive team and a 13-engineer delivery team, it closed about 3,500 pull requests in four months.

This work is under client confidentiality, so there's no public demo. I'm happy to walk through the architecture in a conversation.
