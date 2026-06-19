# Amazon Seller Operations Playbook

This playbook shows how an AI agent can use Amazon Seller MCP for a daily seller-operations review without jumping straight to automated changes.

Use it as an operating checklist for inventory, orders, listings, reports, and performance signals.

## 1. Start Read-Only

Begin each review with read-only data collection:

- Marketplace and seller account scope.
- Active SKUs and ASINs.
- Inventory quantities and stockout risk.
- Recent orders, cancellations, and fulfillment issues.
- Listing status, suppressed listings, and content gaps.
- Sales or business reports relevant to the review period.

Do not create, update, or delete listings until the agent has produced a written action plan and a human approves it.

## 2. Daily Review Flow

Recommended sequence:

1. Check inventory and fulfillment risk.
2. Check orders, cancellations, late shipments, and customer-impacting issues.
3. Check listing health and suppressed or incomplete listings.
4. Pull sales and performance signals for the review window.
5. Identify the top 3 operational risks.
6. Recommend actions with owner, urgency, and expected metric impact.

Output format:

| Area | Signal | Risk | Recommended Action | Approval Needed |
| --- | --- | --- | --- | --- |
| Inventory | SKU has low days of cover | Stockout risk | Prepare reorder or transfer plan | Yes |
| Listings | ASIN suppressed | Lost sales | Fix required attribute or image issue | Yes |
| Orders | Cancellations increased | Account health risk | Review fulfillment workflow | No for analysis, yes for changes |

## 3. Action Boundaries

Classify every recommendation before acting:

| Action Type | Examples | Agent Behavior |
| --- | --- | --- |
| Read-only | Fetch reports, inspect listings, summarize orders | Safe to run during review |
| Draft-only | Generate listing copy, pricing proposal, reorder memo | Safe to draft, do not submit |
| Approval required | Update listing, change inventory, acknowledge workflow action | Ask for explicit current-turn approval |
| Restricted | Delete listings, change account settings, submit irreversible changes | Avoid unless the user has a documented operational procedure |

## 4. Decision Rules

Use these rules to avoid over-automation:

- If data is missing, mark the gap instead of guessing.
- If an action affects customers, inventory, pricing, or account health, require approval.
- If a metric moved, identify the likely cause and the next verification step.
- If several issues appear, rank by revenue risk, account-health risk, and reversibility.
- If an update can be drafted first, draft it before executing it.

## 5. Weekly Business Review Prompt

```text
Use Amazon Seller MCP to prepare a weekly operations review.

Scope:
Marketplace:
Date range:
Priority SKUs or ASINs:
Known issues:

Return:
1. Executive summary
2. Inventory risks
3. Order and fulfillment issues
4. Listing health issues
5. Sales and performance signals
6. Recommended actions
7. Actions requiring approval
8. Missing data
```

## 6. Privacy And Security

- Do not paste credentials, refresh tokens, or raw account exports into prompts.
- Keep customer-identifiable order details out of public issues and pull requests.
- Redact seller IDs, order IDs, addresses, and buyer messages when sharing examples.
- Treat SP-API write operations as production changes.