---
icon: fas fa-book
order: 3
---

The terms I use most, what they mean, and where they show up in my own work.

**Forward deployed engineer (FDE)**
: An engineer who works embedded with a customer's team, owning the path from their problem to working software in production. *In my work:* at FedRock I sit with client executives and delivery teams through discovery, requirements, architecture and release.

**Agentic workflow**
: A process where an AI model plans and takes multi-step actions with tools, not just answers a prompt. *In my work:* Claude Code works Jira tickets end to end and opens pull requests.

**Agent loop (build-and-review loop)**
: A cycle where one agent produces work, another evaluates it, and the first revises until both agree or a limit is hit. *In my work:* Claude Code builds, Codex reviews, capped at 10 rounds as a runaway stop.

**Human in the loop (HITL)**
: A design where a person approves or rejects specific agent actions before they take effect. *In my work:* risky changes wait for an approval, and a human merges every pull request.

**Approval gate**
: A checkpoint in a pipeline that blocks progress until a named condition or person signs off. *In my work:* plan-then-approve before Terraform apply; acceptance criteria, review comments and approval before merge.

**Least-privilege agent access**
: Giving each agent only the credentials and network reach its job needs. *In my work:* scoped tokens per agent, firewalled containers, and a GitHub App identity instead of a personal token.

**Bot identity (GitHub App)**
: A separate, auditable identity an automation acts under, with its own permissions. *In my work:* the Cortex runner and reviewer open and review pull requests as a GitHub App, not as me.

**Custom skill**
: A packaged set of instructions and tools that teaches an agent a repeatable task. *In my work:* 40+ Claude skills covering discovery through operations.

**RAG (retrieval-augmented generation)**
: Grounding a model's answer in documents fetched at query time, usually from a vector database. *In my work:* RAG systems with self-hosted vector databases in AWS and on local infrastructure.

**Fine-tuning**
: Further training an existing model on task-specific data to change its behavior. *In my work:* fine-tuned existing LLMs.

**Self-healing loop**
: An agent loop that detects its own failure, corrects it, and records the lesson for later runs. *In my work:* review findings saved to memory so the same mistake isn't repeated.

**Promotion (dev to prod)**
: Moving a change through environments only after it passes checks in the earlier one. *In my work:* merged n8n workflows deploy to dev automatically, then to production after the dev check passes.

**Infrastructure as code (IaC)**
: Defining infrastructure in versioned code so it can be reviewed, repeated and checked for drift. *In my work:* Terraform/Terragrunt, one module per resource.
