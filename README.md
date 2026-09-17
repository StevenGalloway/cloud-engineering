# Cloud Engineering

This repository demonstrates cloud architecture, deployment, and operational excellence.

---

## Topics
- Infrastructure as Code
- Secure networking & IAM
- Environment automation
- Cost management & tagging
- CI/CD pipelines

---

## Case Studies

| Area | Example |
|-----|--------|
| IaC | Multi-environment deployments |
| Security | Least privilege & secrets |
| Cost | Budgets & guardrails |

---

## Featured external case study: [crm-system](https://github.com/StevenGalloway/crm-system)

A live Azure deployment (Static Web Apps + Functions + Cosmos DB) run at real-world $0-2/month cost. What in that repo actually maps to each topic above:

| Topic | What's actually there |
|---|---|
| **Infrastructure as Code** | [`infra/cosmos-setup.sh`](https://github.com/StevenGalloway/crm-system/blob/main/crm/infra/cosmos-setup.sh) -- scripted Azure CLI provisioning of the resource group, free-tier Cosmos account, database, and both containers with explicit partition keys and throughput; [`infra/seed-config.js`](https://github.com/StevenGalloway/crm-system/blob/main/crm/infra/seed-config.js) for repeatable config-document seeding. Scripted and versioned, not click-ops through the Portal. |
| **CI/CD pipelines** | [azure-static-web-apps.yml](https://github.com/StevenGalloway/crm-system/blob/main/.github/workflows/azure-static-web-apps.yml) for build+deploy, plus a second workflow ([scheduled-jobs.yml](https://github.com/StevenGalloway/crm-system/blob/main/.github/workflows/scheduled-jobs.yml)) standing in for a scheduler the hosting tier doesn't support at all -- a real platform-constraint workaround, not a textbook pipeline (see [ARCHITECTURE.md](https://github.com/StevenGalloway/crm-system/blob/main/crm/ARCHITECTURE.md) §1). |
| **Environment automation** | App behavior (pipeline stages, client partners, owners, notification schedule) lives in a Cosmos config document, editable live via the app's own Configuration page or `PUT /api/config` -- zero redeploys for day-to-day changes. |
| **Cost management & tagging** | Deliberately free-tier-first: Cosmos DB free tier, Static Web Apps free tier, Functions Consumption plan. Cost tradeoffs are called out explicitly in the app's own README rather than left as a surprise. |
| **Secure networking & IAM** | **Honest gap, not a highlight:** this app uses key-based Cosmos auth (`COSMOS_KEY` as an Application Setting) with no Managed Identity/RBAC, and no VNet or private endpoints -- a deliberate, documented scope call for a $0-2/month POC, not something to overclaim on a cloud-engineering repo. |

---

## Structure
- `case-studies/`
- `infra/`
- `pipelines/`
- `docs/`
