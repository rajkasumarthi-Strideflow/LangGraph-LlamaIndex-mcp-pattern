# Synthetic Field Sales Scenarios

These scenarios use synthetic data only. They are intended for public-safe demos and future golden-scenario evaluation.

## 1. Missing Account/Product Details -> Clarification

**Rep request:**

> “Can you help me build a quote for helmets?”

**Expected outcome:**

The router should ask for missing account, quantity, and product configuration details. The governed quote workflow should not start until required facts are available.

## 2. Unsupported Color/Product Combination -> Blocked

**Rep request:**

> “Build a quote for 50 varsity helmets in chrome purple for Westlake High School.”

**Expected outcome:**

The RAG layer should retrieve product/spec evidence showing the requested color is unsupported for the product. Guardrails should block draft quote creation or route to an exception path.

## 3. Inventory Unavailable -> Approval/Escalation or Alternative Suggestion

**Rep request:**

> “Westlake High School needs 80 varsity helmets in matte navy by next week.”

**Expected outcome:**

Inventory check should identify insufficient availability. The workflow should avoid creating a misleading draft quote and instead escalate or suggest an alternative quantity/timeline.

## 4. Discount Above Approval Threshold -> Approval Required

**Rep request:**

> “Build a quote for 50 varsity helmets and apply a 20 percent discount.”

**Expected outcome:**

Pricing rules should detect that 20 percent exceeds the manager approval threshold. The workflow should mark approval required and avoid presenting the quote as final.

## 5. Valid Quote Request -> Draft Quote Created

**Rep request:**

> “I’m meeting Westlake High School about helmets and jerseys. They want 50 varsity helmets in matte navy and matching jerseys. Build a draft quote with the standard booster club discount.”

**Expected outcome:**

The workflow should retrieve account context, product/spec evidence, inventory, and pricing rules. If all guardrails pass, it should create a draft quote and produce a rep-facing summary with caveats.
