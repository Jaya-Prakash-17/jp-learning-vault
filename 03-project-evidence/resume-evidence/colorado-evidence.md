# State of Colorado Project Resume Evidence

## Bullet Point 1
**"Engineered complex MapBuilder logic for inbound 837 Institutional and Professional claims, ensuring strict compliance with State Medicaid guidelines."**

- **Actual Work Performed**: Designed the translation layer that converted heavily nested, batch X12 837 claims into the flat XML format required by the State of Colorado's backend Medicaid adjudication engine.
- **Technical Details**: Edifecs MapBuilder, SpecBuilder (SNIP 1 & 2 validation), Hierarchical Loop traversal (2000A/B/C), Conditional `If-Exists` logic, Data Type casting.
- **Possible Interview Questions**: 
  - "How do you handle mapping a repeating X12 segment, like multiple service lines on a single claim?"
  - "What happens if a provider submits a claim missing an optional segment?"
- **Strong Answer**: "For repeating segments like the 2400 Service Line, I implemented `For-Each` loops in MapBuilder to iterate through the X12 nodes and generate a corresponding array of XML elements. For optional segments, I wrapped my mapping paths in strict `If-Exists` conditionals to prevent Null Pointer Exceptions, ensuring the pipeline remained robust even with sparse data."
- **Red Flags To Avoid**: Describing MapBuilder as just "drag and drop." You must emphasize the underlying logical control structures (Loops, Conditionals, Type Casting) you implemented.
- **Evidence Supporting Claim**: Successful processing of 837 batch files triggering 100% compliant 999 acceptances and 277CA receipts during UAT (User Acceptance Testing).

---

## Bullet Point 2
**"Configured and deployed SpecBuilder profiles to automate front-door SNIP Level 1 and 2 validations."**

- **Actual Work Performed**: Cloned baseline HIPAA implementation guides in SpecBuilder and customized them to match the specific quirks and requirements of Colorado Medicaid trading partners.
- **Technical Details**: SNIP validations, Custom Business Rules, Profile Export (`.ecs`), Route integration.
- **Possible Interview Questions**: 
  - "Have you ever had to relax a SNIP rule for a trading partner?"
- **Strong Answer**: "Yes. Sometimes massive clearinghouses refuse to fix a minor structural error on their end. To prevent millions of dollars in claims from being rejected at the front door, I cloned the baseline profile in SpecBuilder, relaxed that specific SNIP 2 length-validation rule, and updated my MapBuilder logic downstream to handle the anomaly safely."
- **Red Flags To Avoid**: Implying that SNIP validation fixes all data issues. (SNIP only checks structure; MapBuilder/Groovy must handle the business transformation).
- **Evidence Supporting Claim**: Drastic reduction in false-positive 999 rejections after custom profile deployment.
