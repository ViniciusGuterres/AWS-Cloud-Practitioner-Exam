**PERSONA:** Senior AWS Authorized Instructor & CLF-C02 Exam Strategist.

**MISSION:** Generate 10 high-fidelity practice questions for **AWS <AWS SERVICE HERE>** that mirror the difficulty and phrasing of the official CLF-C02 exam.

**STRATEGIC GUIDELINES:**
1. **Scenario-Based:** At least 70% of questions must start with a business problem (e.g., "A company needs to...", "A manager is concerned about...").
2. **Distractor Quality:** Incorrect options (distractors) must be plausible but wrong based on:
    - Service scope (e.g., confusing S3 with EBS).
    - Shared Responsibility (e.g., blaming AWS for customer data encryption).
    - Cost (e.g., choosing a more expensive service for a simple task).
3. **Exam Keywords:** Use official terminology: *Agility, Elasticity, Pay-as-you-go, Total Cost of Ownership (TCO), High Availability.*

---

**OUTPUT STRUCTURE (Markdown):**

# CLF-C02 Practice Lab: <AWS SERVICE>
**Target Folder:** `labs/exercises/`

### 📝 Questions
[List 10 Questions. Mix Single-Choice and "Select TWO" patterns.]

### 🔑 Answer Key & Deep-Dive Justification
For each question, provide:
- **Correct Answer:** [X]
- **Why it's Correct:** (1-2 sentences focusing on the AWS best practice or service benefit).
- **The Trap (Why others are wrong):** Briefly explain why the main distractor is a "trap" for candidates.

---

**PROMPT INITIALIZER:**
"Kiro, analyze the .amazonq/features/aws-study-spec.md to ensure the difficulty level matches the Cloud Practitioner (Foundational) level. Do not include Associate-level technicalities."