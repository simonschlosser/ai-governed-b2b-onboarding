# AI-Governed B2B Onboarding (Signals → Policy → Explanation)

This repository contains a reference implementation of a governed onboarding workflow using:

- CDQ services for authoritative signal generation
- n8n Cloud for orchestration and policy routing
- Bounded AI for structured review explanations

The design follows the pattern:

Signals → Policy → Explanation

AI does not decide compliance outcomes.
It explains decisions after deterministic policy has been applied.

---

## Architecture Overview

### 1. Signals
- CDQ Lookup (entity resolution)
- CDQ AML Guard (sanctions screening)

Each service produces structured, auditable evidence.

### 2. Policy
- Deterministic identity banding
- Clear winner logic
- AML routing
- Explicit decision states: PROCEED / REVIEW / REQUEST_INFO

Policy is implemented in n8n via Function and Switch nodes.

### 3. Explanation
When a case is routed to REVIEW:
- AI generates a structured review card
- No policy is embedded in the model
- Outputs remain logged and reproducible

---

## Workflow Components

The workflow includes:

1. Webhook trigger
2. Input normalization
3. CDQ Lookup API call
4. Identity banding logic
5. Optional AI identity resolution (middle band)
6. CDQ AML screening
7. Deterministic routing
8. AI review card generation (review cases only)
9. Structured webhook response

---

## Setup Instructions

1. Import `workflow/onboarding-workflow.json` into n8n Cloud.
2. Configure credentials:
   - CDQ API Key
   - OpenAI API Key
3. Set the webhook URL in your test client.

---

## Example Request

```json
{
  "companyName": "CDQ AG",
  "country": "DE"
}
