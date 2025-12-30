# Meta Compliance QA Agent - User Guide

## Quick Start

**Invoke with natural language:**
```
"Review this Facebook ad for meta compliance"
"Check if this CBD product ad meets Instagram requirements"
"Validate this weight loss ad against Meta policies"
```

**Or use explicit triggers:**
- `meta compliance`
- `facebook ad compliance`
- `instagram ad review`
- `meta policy check`

---

## What This Agent Does

The **meta-compliance-qa** agent validates advertising content against Meta platform (Facebook, Instagram) compliance requirements before submission. It analyzes:

- **Ad copy** - Text content for prohibited claims, substances, discriminatory language
- **Visual content** - Images for before/after comparisons, negative self-perception, prohibited imagery
- **Targeting settings** - Age restrictions, geographic limitations
- **Product classification** - Determines restriction level and required certifications
- **Business assets** - Validates business information, landing pages, lead ad compliance

**Output:** Structured compliance report with severity-classified violations, actionable corrections, and approval decision.

---

## When to Use This Agent

### Auto-Activates When:

**File Patterns:**
- Working in `**/facebook-ads/**` directories
- Working in `**/instagram-ads/**` directories
- Working in `**/meta-ads/**` directories
- Files ending with `*-ad-copy.md`
- Files ending with `*-creative-brief.md`

**Content Keywords:**
- "Meta Ad Library"
- "Facebook advertising"
- "Instagram promotion"
- "LegitScript"
- "weight loss supplement"
- "CBD product"
- "prescription medication"

### Manual Activation:

Use when you need to validate:
- Health supplement ads
- Weight loss product ads
- CBD product ads
- Prescription drug ads
- Cosmetic procedure ads
- Wellness product ads

---

## How to Use

### Basic Usage

**Example 1: Quick text validation**
```
"Review this ad copy for Meta compliance:

Transform your body in 30 days! Our CBD weight loss formula
helps you lose 20 pounds fast. See amazing before/after results!"
```

**Example 2: Complete ad package validation**
```
"Validate this CBD product ad for Meta:

Product: CBD Sleep Drops
Ad Copy: Fall asleep faster with our premium CBD oil
Target Audience: Adults 21+, United States only
Certifications: LegitScript certified, Meta authorization approved
THC Content: 0.2%
Image: Product bottle on nightstand (no people, no before/after)"
```

**Example 3: With targeting settings**
```
"Check Meta compliance for this ad:

Product: Weight loss supplement
Copy: 'Clinically proven fat burner. Results in 2 weeks!'
Targeting: Age 25-45, United States + Canada
Image: Close-up of measuring tape around waist"
```

### Input Format

Provide as much detail as possible:

**Required:**
- Ad copy (text content)
- Product category/type

**Highly Recommended:**
- Target age range
- Target countries/regions
- Image descriptions or URLs
- THC content (for CBD/hemp products)
- Certification status (LegitScript, Meta authorization)

**Optional but Helpful:**
- Business name
- Landing page URL
- Lead ad form details
- Previous rejection reasons

---

## Understanding the Output

### Report Structure

```markdown
# Meta Compliance Review Report

**Overall Status**: APPROVED / CONDITIONAL / REJECTED

## Critical Violations (Immediate Rejection Required)
[CSAM, dangerous orgs, discrimination, hate, exploitation, misinformation, fraud, illicit drugs, THC products]

## High Priority Issues (Must Fix Before Approval)
[Missing certifications, wrong targeting, prohibited substances, sex toys, skin lightening]

## Medium Priority Issues (Corrections Required)
[Age targeting errors, before/after imagery, health claims violations, adult nudity, profanity]

## Low Priority Recommendations
[Best practice violations, optimization opportunities]

---

## Compliance Checklist

### Age Targeting
- [ ] Product requires 18+ targeting: YES/NO
- [ ] Current targeting setting: [age range]
- [ ] Status: PASS/FAIL

### Geographic Restrictions
- [ ] Product has geographic restrictions: YES/NO
- [ ] Allowed countries: [list]
- [ ] Current targeting: [countries]
- [ ] Status: PASS/FAIL

### Certification Requirements
- [ ] LegitScript certification required: YES/NO
- [ ] LegitScript certification status: VERIFIED/MISSING/N/A
- [ ] Meta authorization required: YES/NO
- [ ] Meta authorization status: VERIFIED/MISSING/N/A
- [ ] Status: PASS/FAIL

### Visual Content
- [ ] Contains before/after comparisons: YES/NO
- [ ] Contains negative self-perception: YES/NO
- [ ] Contains prohibited visuals: YES/NO
- [ ] Status: PASS/FAIL

### Claims Validation
- [ ] Contains health claims: YES/NO
- [ ] Health claims compliant: YES/NO/N/A
- [ ] Contains prohibited substances: YES/NO
- [ ] Status: PASS/FAIL

---

## Recommended Actions
1. [Specific action with file/line reference]
2. [Specific action with file/line reference]

## Approval Decision
**Decision**: APPROVED / CONDITIONAL APPROVAL / REJECTED
**Reasoning**: [Brief explanation]
**Next Steps**: [What to do next]
```

### Severity Levels Explained

**CRITICAL → REJECT_IMMEDIATELY**
- Absolute policy violations with no exceptions
- Examples: CSAM, dangerous organizations, discrimination, hate speech, human exploitation, health misinformation, vaccine discouragement, fraud, illicit drugs, THC products
- **Action:** Ad cannot run - must completely change content or abandon campaign

**HIGH → BLOCK_UNTIL_FIXED**
- Required certifications missing or geographic violations
- Examples: Missing LegitScript certification, no Meta authorization, wrong country targeting, prohibited substances, sex toys
- **Action:** Must obtain certifications or fix targeting before approval

**MEDIUM → REQUIRE_CORRECTION**
- Policy violations that can be corrected with content changes
- Examples: Wrong age targeting, before/after imagery, health claims on CBD, negative self-perception tactics
- **Action:** Revise copy/imagery and resubmit for approval

**LOW → RECOMMEND_IMPROVEMENT**
- Best practice violations and optimization opportunities
- Examples: Unclear business info, non-optimal targeting, messaging improvements
- **Action:** Optional improvements to increase approval chances and performance

---

## Validation Workflow

The agent performs **5-phase sequential validation**:

### Phase 1: Content Analysis (CRITICAL)
- Scans for absolute prohibitions (CSAM, dangerous orgs, hate, fraud, illicit drugs)
- Classifies product category (determines which rules apply)

### Phase 2: Restriction Validation (CRITICAL)
- Verifies age targeting (18+ for restricted products)
- Validates geographic restrictions (US/Canada/NZ for prescription drugs, US-only for CBD)
- Checks certification requirements (LegitScript, Meta authorization)

### Phase 3: Visual Content Analysis
- Detects before/after weight loss comparisons
- Identifies negative self-perception imagery
- Flags prohibited visuals (adult nudity, graphic violence)

### Phase 4: Claims Validation (CRITICAL)
- Validates health claims (CBD cannot claim medical benefits)
- Verifies substance content (THC <0.3%, no prohibited substances)
- Assesses product claims accuracy

### Phase 5: Business Asset Validation
- Checks business information completeness
- Validates lead ad restrictions (no credit cards, payday loans, political donations)

---

## Common Scenarios

### Scenario 1: Weight Loss Supplement

**Input:**
```
"Validate this weight loss ad for Meta:

Product: Fat Burner Pro
Copy: 'Lose 15 pounds in 30 days! Clinical results proven.'
Targeting: Age 25-54, United States
Image: Before/after side-by-side transformation photos"
```

**Expected Output:**
```markdown
**Overall Status**: REJECTED

## Medium Priority Issues
1. **Before/After Imagery**: Side-by-side weight loss comparisons prohibited
   unless for fitness class workout results
2. **Unrealistic Claims**: "Lose 15 pounds in 30 days" may constitute
   false or misleading health claims

## Compliance Checklist
### Age Targeting
- [x] Product requires 18+ targeting: YES (weight loss supplement)
- [x] Current targeting: 25-54
- [x] Status: PASS

## Recommended Actions
1. Remove before/after side-by-side imagery
2. Revise weight loss timeline to realistic expectations
3. Add "results may vary" disclaimer
4. Replace absolute guarantees with evidence-based claims

## Approval Decision
**Decision**: REJECTED
**Reasoning**: Before/after imagery violation + unrealistic health claims
**Next Steps**: Remove comparison imagery, substantiate claims, resubmit
```

### Scenario 2: CBD Product

**Input:**
```
"Check this CBD ad for Instagram compliance:

Product: CBD Anxiety Relief Tincture
Copy: 'Premium CBD oil helps reduce anxiety and improve sleep naturally.'
Targeting: Age 21+, United States only
Certifications: LegitScript certified, Meta authorization approved
THC: 0.2%"
```

**Expected Output:**
```markdown
**Overall Status**: CONDITIONAL APPROVAL

## Medium Priority Issues
1. **Health Claims**: "helps reduce anxiety and improve sleep" constitutes
   medical claims. CBD cannot claim to diagnose, cure, mitigate, treat,
   or prevent diseases or medical conditions.

## Compliance Checklist
### Age Targeting
- [x] Product requires 18+ targeting: YES
- [x] Current targeting: 21+
- [x] Status: PASS

### Geographic Restrictions
- [x] Product has geographic restrictions: YES (US only)
- [x] Allowed countries: United States
- [x] Current targeting: United States
- [x] Status: PASS

### Certification Requirements
- [x] LegitScript certification required: YES
- [x] LegitScript certification status: VERIFIED
- [x] Meta authorization required: YES
- [x] Meta authorization status: VERIFIED
- [x] Status: PASS

### Claims Validation
- [x] Contains health claims: YES
- [ ] Health claims compliant: NO
- [x] Contains prohibited substances: NO (THC 0.2% < 0.3% limit)
- Status: FAIL

## Recommended Actions
1. Remove medical claims ("reduce anxiety", "improve sleep")
2. Use general wellness language: "supports overall wellness", "promotes relaxation"
3. Focus on product quality and ingredients without health benefit claims

## Approval Decision
**Decision**: CONDITIONAL APPROVAL
**Reasoning**: Certifications and targeting correct, but health claims must be removed
**Next Steps**: Revise ad copy to remove prohibited claims, then resubmit
```

### Scenario 3: Prescription Drug (Clean)

**Input:**
```
"Meta compliance check for prescription drug ad:

Product: Blood pressure medication (prescription)
Copy: 'Talk to your doctor about managing hypertension. Prescription required.'
Targeting: Age 35+, United States
Certifications: LegitScript certified online pharmacy, Meta authorization approved"
```

**Expected Output:**
```markdown
**Overall Status**: APPROVED

## Critical Violations
None detected

## High Priority Issues
None detected

## Medium Priority Issues
None detected

## Low Priority Recommendations
None - ad follows all compliance requirements

## Compliance Checklist
### Age Targeting
- [x] Product requires 18+ targeting: YES
- [x] Current targeting: 35+
- [x] Status: PASS

### Geographic Restrictions
- [x] Product has geographic restrictions: YES (US/Canada/NZ only)
- [x] Allowed countries: United States, Canada, New Zealand
- [x] Current targeting: United States
- [x] Status: PASS

### Certification Requirements
- [x] LegitScript certification required: YES
- [x] LegitScript certification status: VERIFIED
- [x] Meta authorization required: YES
- [x] Meta authorization status: VERIFIED
- [x] Status: PASS

## Approval Decision
**Decision**: APPROVED
**Reasoning**: All certifications verified, correct geographic targeting,
appropriate age restrictions, compliant messaging
**Next Steps**: Ad approved for submission to Meta
```

---

## Integration with Other Agents

### Copychief Collaboration

The meta-compliance-qa agent works seamlessly with the **copychief** agent for copy optimization:

**Workflow:**
1. **Copychief** optimizes ad copy for conversion and engagement
2. **Meta-compliance-qa** validates compliance before submission
3. Iterate until both conversion optimization AND compliance are satisfied

**Example:**
```
"Use copychief to optimize this weight loss ad copy, then validate
with meta-compliance-qa before we submit to Facebook"
```

### Marketing-Validator-Compliance

For **cross-platform compliance** (FTC, FDA, GDPR requirements):

**Workflow:**
1. **Meta-compliance-qa** validates Meta-specific policies
2. **Marketing-validator-compliance** validates regulatory compliance (FTC, FDA)
3. Ensures both platform policies AND legal regulations are met

---

## Best Practices

### 1. Validate Early
Run compliance checks BEFORE finalizing creative assets. Catching violations early saves time and redesign costs.

### 2. Provide Complete Context
The more information you provide, the more accurate the validation:
- Include targeting settings (age, countries)
- Specify certification status (LegitScript, Meta authorization)
- Describe images in detail or provide URLs
- Include THC content for CBD/hemp products
- Mention any previous rejections or concerns

### 3. Understand Severity Levels
- **CRITICAL/HIGH:** Must fix or campaign cannot run
- **MEDIUM:** Should fix to avoid rejection
- **LOW:** Optional improvements for better performance

### 4. Geographic Targeting Matters
Always specify target countries, especially for:
- Prescription drugs (restricted to US/Canada/NZ)
- CBD products (US only)
- Hemp products (US/Canada/Mexico)

### 5. Age Targeting is Mandatory
Restricted products MUST target 18+ years:
- Weight loss products
- Cosmetic procedures
- Skin care (anti-aging)
- Adult wellness products
- Prescription drugs
- OTC drugs
- CBD products
- Alcohol, tobacco, weapons

### 6. Certifications Cannot Be Skipped
For prescription drugs and CBD products, you MUST have:
1. **LegitScript certification** (apply at LegitScript.com)
2. **Meta written authorization** (apply after LegitScript approval)

Without both certifications, ads will be rejected regardless of content quality.

### 7. Visual Content Rules
**Prohibited:**
- Before/after weight loss side-by-side images
- Close-ups of pinching body fat
- Before/after wrinkle treatment comparisons
- Body shaming or negative self-perception imagery

**Exception:** Fitness classes can show workout transformation results

### 8. CBD Health Claims
CBD products CANNOT claim to:
- Diagnose diseases
- Cure diseases
- Mitigate diseases
- Treat diseases
- Prevent diseases

**Allowed:** "Supports overall wellness", "promotes relaxation" (general wellness language)

---

## Troubleshooting

### "Why was my ad rejected as CRITICAL?"
Check for prohibited content:
- Illicit drugs, THC products, drug paraphernalia
- Discriminatory practices
- Hateful conduct
- Misinformation (health, climate, election)
- Fraud or scams

These violations have zero tolerance - content must be completely changed.

### "I have LegitScript but still got rejected"
Verify:
1. **Meta authorization:** LegitScript alone is not enough - you also need Meta written authorization
2. **Geographic targeting:** Are you targeting allowed countries only?
3. **Health claims:** Even with certifications, you cannot make prohibited medical claims (especially CBD)

### "My fitness class ad was rejected for before/after images"
Ensure the context is clear:
- Images should show workout/exercise environment
- Context should emphasize fitness class participation
- Avoid pure weight loss framing - emphasize fitness achievement

### "What counts as 'negative self-perception'?"
Content that:
- Makes viewers feel inadequate about their appearance
- Uses body shaming language or imagery
- Implies viewers "need" the product to be acceptable
- Focuses on flaws or deficiencies
- Creates comparison anxiety

---

## Advanced Usage

### Batch Validation

**Validate multiple ads:**
```
"Review these 3 Meta ads for compliance:

Ad 1: [content]
Ad 2: [content]
Ad 3: [content]"
```

The agent will provide individual compliance reports for each ad.

### Integration with Workflow

**End-to-end ad development:**
```
1. "Use copychief to write compelling ad copy for CBD sleep product"
2. "Now validate that copy with meta-compliance-qa"
3. "Use ux-designer to create compliant ad creative mockups"
4. "Final compliance check with meta-compliance-qa before submission"
```

### Policy Research

**Check specific rules:**
```
"What are Meta's requirements for advertising prescription drugs?"
"Can I show before/after images for a fitness class?"
"What certifications do I need for CBD product ads?"
```

The agent can answer policy questions by referencing its comprehensive compliance ruleset.

---

## Quick Reference

### Products Requiring 18+ Targeting
✓ Weight loss products
✓ Cosmetic procedures
✓ Skin care (anti-aging)
✓ Adult wellness
✓ Prescription drugs
✓ OTC drugs
✓ CBD products
✓ Alcohol
✓ Tobacco
✓ Weapons

### Products Requiring LegitScript Certification
✓ Prescription drug advertisers
✓ Online pharmacies
✓ Telehealth providers
✓ Pharmaceutical manufacturers
✓ CBD product advertisers

### Geographic Restrictions
| Product | Allowed Countries |
|---------|-------------------|
| Prescription drugs | US, Canada, New Zealand |
| CBD products | United States only |
| Hemp products (non-CBD) | US, Canada, Mexico |

### Prohibited Substances
❌ Illicit drugs (cocaine, heroin, meth, etc.)
❌ Recreational drugs
❌ THC products / cannabis with psychoactive components
❌ Drug paraphernalia
❌ Anabolic steroids
❌ Chitosan, Comfrey, DHEA, Ephedra, HGH

### Visual Content Red Flags
❌ Before/after weight loss side-by-side
❌ Body fat pinching close-ups
❌ Wrinkle treatment before/after
❌ Body shaming imagery
❌ Negative self-perception
❌ Adult nudity (without artistic/educational context)
❌ Graphic violence

### CBD-Specific Rules
✓ Must be US-only targeting
✓ Must target 18+ years
✓ Must have LegitScript certification
✓ Must have Meta written authorization
✓ THC content must be <0.3%
❌ Cannot claim to diagnose, cure, mitigate, treat, or prevent diseases
❌ Cannot make unsubstantiated health claims

---

## Performance Expectations

- **Response Time:** <5 seconds for text analysis
- **Accuracy:** >95% violation detection rate
- **False Positives:** <5%

---

## Token Budget

**Estimated:** 35k tokens per review
**Complexity:** High (multi-phase validation, visual analysis, regulatory compliance)
**Auto@Files:** 30 files

For large batch validations, consider processing in groups of 3-5 ads to manage context efficiently.

---

## Support and Updates

### Policy Updates
This agent's compliance rules are updated when Meta publishes policy changes through:
- Meta Transparency Center updates
- Community Standards changes
- LegitScript certification requirement updates
- FDA/FTC regulatory changes

### Getting Help
For questions about specific policy interpretations or complex scenarios:
```
"Explain Meta's policy on [specific topic]"
"What's the rule for [specific situation]?"
```

### Feedback
If the agent incorrectly flags or misses a violation:
- Document the specific case
- Include the ad content and validation result
- Note the expected vs actual outcome
- This helps improve detection accuracy

---

## Related Documentation

- **Compliance Rules:** `/output/meta_advertising_compliance_rules.md` - Complete policy reference
- **Agent Design:** `.claude/agents/meta-compliance-qa.md` - Technical architecture
- **Agent Config:** `.claude/agents/meta-compliance-qa.yaml` - Machine-readable configuration
- **Project Tracking:** `_ops/PROGRESS.md` - Development status

---

## Examples from Real Use Cases

### Example 1: Clean Approval

**Input:**
```
"Validate for Meta:
Product: Vitamin D supplement
Copy: 'Premium Vitamin D3 for daily wellness. Made in USA.'
Targeting: Age 25+, United States
Image: Product bottle on white background"
```

**Result:** ✅ **APPROVED** - No violations, ready for submission

---

### Example 2: Multiple Violations

**Input:**
```
"Check this ad:
Product: CBD pain relief cream
Copy: 'Cures arthritis pain! Doctor recommended. Works in 24 hours!'
Targeting: Age 18+, United States + Canada
Certifications: None
Image: Before/after pain scale comparison"
```

**Result:** ❌ **REJECTED**

**Issues:**
- HIGH: Missing LegitScript certification
- HIGH: Wrong geographic targeting (Canada not allowed for CBD)
- MEDIUM: Prohibited health claims ("Cures arthritis pain")
- MEDIUM: Before/after comparison imagery

---

### Example 3: Conditional Approval

**Input:**
```
"Validate:
Product: Natural sleep aid (non-CBD)
Copy: 'Fall asleep naturally with melatonin + chamomile blend'
Targeting: Age 21+, United States
Image: Person sleeping peacefully"
```

**Result:** ✅ **CONDITIONAL APPROVAL**

**Issues:**
- LOW: Consider adding "Consult physician" disclaimer for best practices

**Next Steps:** Optional improvements recommended, but ad is compliant and ready for submission

---

## Summary

The meta-compliance-qa agent is your pre-submission compliance validator for Meta advertising. It catches violations before you submit, saving rejection time and ensuring your ads meet all platform requirements.

**Use it whenever you're advertising:**
- Health/wellness products
- CBD products
- Prescription drugs
- Weight loss products
- Cosmetic procedures
- Any restricted product category

**Trust the severity levels:**
- CRITICAL/HIGH = must fix or ad cannot run
- MEDIUM = should fix to avoid rejection
- LOW = optional improvements

**Provide complete context for best results** - the more targeting, certification, and visual details you include, the more accurate the validation.
