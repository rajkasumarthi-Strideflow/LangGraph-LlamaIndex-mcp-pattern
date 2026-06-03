# Field Sales Agent Rollout and Rollback

## Controlled Rollout Pattern

Field Sales Agent should be introduced through controlled validation gates rather than broad release on day one.

## 1. Local Validation

- Run deterministic unit and workflow tests.
- Validate golden scenarios.
- Check API contract examples.
- Confirm no secrets or real customer data are included.

## 2. Golden Scenario Evaluation

Golden scenarios should validate:

- Clarification behavior
- Product/spec grounding
- Inventory handling
- Discount guardrails
- Approval thresholds
- Draft-only quote behavior
- Audit and cost telemetry capture

## 3. Staging Deployment

Deploy to a staging environment with synthetic data and test credentials only. Review monitoring dashboards, audit replay, and cost telemetry before broader demo rollout.

## 4. Limited Demo Rollout

Expose the demo to a small set of reviewers. Monitor workflow outcomes, guardrail decisions, cost telemetry, and any unexpected responses.

## 5. Monitoring Checks

Track:

- Workflow success and failure rates
- Guardrail block/allow/approval outcomes
- Cost per attempt
- Retrieval evidence availability
- Tool failure rates
- Audit event completeness

## 6. Rollback Triggers

Rollback if any of the following occur:

- Draft quote created without required evidence
- Final order or shipment implied
- Unsupported product claim appears in rep summary
- Discount guardrails fail
- Audit events missing for critical decisions
- Cost telemetry missing or clearly incorrect
- Repeated workflow failures after deployment

## 7. Rollback Steps

- Disable new demo workflow version.
- Restore previous known-good version.
- Preserve audit, trace, and cost records.
- Notify stakeholders.
- Convert failure into regression scenario.

## 8. Post-Rollback Audit Review

Review audit events, traces, prompt/tool behavior, and guardrail outcomes. The expected improvement loop is:

```text
failure -> audit/trace review -> regression scenario -> fix -> validation -> redeploy
```
