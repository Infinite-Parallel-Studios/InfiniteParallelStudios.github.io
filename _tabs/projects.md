---
icon: fas fa-diagram-project
order: 1
---

Each project gets a write-up in the shape I'd use to walk an engineering team through it: the problem, the architecture, the decisions and trade-offs, how it fails, and what I learned. Where a project can be shown, it has a demo.

Projects are grouped by where they stand: **Shipped** is running today. **In progress** is partly built. **Planned** is designed, with the build ahead.

## Shipped

### Infinite Cortex

<span class="badge bg-success">Shipped</span> *Personal project · Self-hosted AI agent orchestration platform*

A self-hosted platform where a Claude Code runner takes Jira tickets in dependency order, opens pull requests under a GitHub App bot identity, and a Codex reviewer in its own container reviews each one before a human merges. Workflows ship automatically from dev to production after a dev check, and risky changes wait on a human approval.

**Stack:** Claude Code, Codex, n8n, Jira, GitHub Apps, PostgreSQL, Ollama, Proxmox containers

{% include demo.html video="" caption="Infinite Cortex: one ticket from Jira to a reviewed, merged pull request" %}

[Read the case study]({% post_url 2026-10-29-infinite-cortex %})

### AI delivery system for client engagements

<span class="badge bg-success">Shipped</span> *Client work at FedRock · Clients named by industry only*

An AI-driven delivery workflow built from 40+ custom Claude skills that run the full lifecycle, from discovery intake and SOWs through architecture, Terraform, Jira ticket breakdown, coding, review, QA, release and operations, with human approval gates at each step. Claude Code writes most of the code, Codex reviews every pull request against coding standards, and a merge-when-ready queue merges pull requests one at a time once acceptance criteria, review comments and human approval are met.

Teams using the system merged ~30,000 pull requests across client engagements in 2026. On one engagement, forward deployed with a luxury-goods client's executive team and a 13-engineer delivery team, it closed about 3,500 pull requests in four months.

This work is under client confidentiality, so there's no public demo. I'm happy to walk through the architecture in a conversation.

## In progress

### USA Guppies: an AI-managed commerce business

<span class="badge bg-warning text-dark">In progress</span> *Personal business · Family-owned fish breeding in Georgia*

USA Guppies breeds US-raised guppies, shrimp and aquarium plants. The goal is a store that an AI assistant runs end to end: one storefront as the main funnel, the same catalog listed across as many marketplaces as possible, and every social post and video pointing traffic back to it.

- **Storefront:** moving the existing site to Shopify, with Claude connected to build and manage the store. The replica homepage is built.
- **Catalog:** guppies, shrimp, plants and dried goods, each listing with its own photos and a video from the USA Guppies YouTube channel.
- **Customer insight:** a strain request poll where visitors name the strains they want, feeding what gets bred next.
- **Marketplaces:** listings beyond the storefront, such as eBay, with the storefront handling fulfillment.
- **End state:** Infinite Cortex manages the store, listings and infrastructure, with a human approving anything that spends money or reaches customers.

{% include demo.html video="" caption="USA Guppies: the AI-managed storefront" %}

## Planned

### Cortex delivery skill chain

<span class="badge bg-secondary">Planned</span> *Personal project · Extends Infinite Cortex*

A chain of 41 skills that takes a software project from first conversation to production and operations, with a human decision at each step. It's modeled on the delivery workflow I built for client work and rebuilt for Cortex.

- **Infrastructure:** intake interview and master plan, infrastructure baseline and architecture sign-off, one Terraform module per resource, ticket breakdown with dependency ordering, account provisioning with credentials in a vault, bootstrap with compliance controls, plan and approval, apply, and drift and compliance validation.
- **Application:** an orchestrator that bootstraps each language stack, and an SDLC planning agent that turns requirements into a reviewed Jira epic.
- **Source control and CI/CD:** pipeline skills for GitHub and GitLab, and repo governance with a base guardrail set plus CMMC and HIPAA add-on packs.
- **Build, review and merge:** work skills by area, Codex review on every pull request, a fix loop that escalates disagreements to a human, and a merge-when-ready queue.
- **Deploy, QA and release:** deploy to dev, skill-driven QA and bug fixing, scheduled releases, and production QA.
- **After launch:** new-feature runs through the full chain, testing by app type, security scanning in CI, cost and utilization reviews, container builds, and network connectivity.
- **Operations and business:** monitoring and alerting, backup and restore testing, incident runbooks, database migrations, secrets rotation, client handover, cost alerts, stakeholder reports, SOWs and invoices.

{% include demo.html video="" caption="Cortex skill chain: from intake interview to a production release" %}

### Content, social media and video pipeline

<span class="badge bg-secondary">Planned</span> *Personal businesses · USA Guppies and real estate*

One pipeline for the YouTube channels and social accounts behind my businesses: AI-assisted video editing, cutting long videos into short clips, writing titles and descriptions, and scheduling posts across platforms, with each piece linking back to the right storefront or listing.

{% include demo.html video="" caption="Content pipeline: one recording to published videos and posts" %}

### Lead generation and automation

<span class="badge bg-secondary">Planned</span> *Personal businesses · Real estate and USA Guppies*

Inbound lead generation that doesn't depend on cold calls: content brings people in, n8n workflows capture and route each lead, and an AI assistant handles the first follow-up and books a call, with a human taking it from there. The same automation layer triages email and keeps every project's work moving through Jira.

{% include demo.html video="" caption="Lead generation: from a post to a booked call" %}

### Infinite Realty Hub

<span class="badge bg-secondary">Planned</span> *Personal project · Runs on Infinite Cortex*

An AI assistant for the real estate industry, built for agents, brokers and teams, with my own brokerage as its first user. It uses Infinite Cortex as its backbone.

{% include demo.html video="" caption="Infinite Realty Hub" %}
