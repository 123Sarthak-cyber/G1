# Implementation Guide: Threat and Benefit Frame Annotation
**Following the bacchuss Annotation Routine**

---

## STEP 1: PREPARE YOUR TEXT INPUT

### 1.1 Text Format Requirements
- One paragraph per annotation unit
- Save your text paragraphs in one of these formats:
  - Plain text file (one paragraph per line)
  - CSV with column labeled "paragraph" or "text"
  - JSON array with objects containing "paragraph" field

### Example Input (CSV):
```
id,paragraph
1,"The new trade agreement threatens to reduce domestic manufacturing capacity and puts workers at risk."
2,"Investment in renewable energy creates jobs while reducing long-term energy costs for consumers."
3,"Economic data shows stable growth trajectory with unemployment rates stable at historical averages."
```

---

## STEP 2.1: TEST DRAFT ANNOTATIONS - INITIAL SAMPLE

### Workflow:
1. **Select test sample:** Choose 5-10 diverse paragraphs (easy, ambiguous, mixed cases)
2. **Run initial annotation:** Use the annotation instructions to analyze each paragraph
3. **Visual inspection checklist:**
   - [ ] Which cases were correctly labeled for threat?
   - [ ] Which cases were correctly labeled for benefit?
   - [ ] Are there missing threat/benefit cases the instructions don't capture?
   - [ ] Are there false positives (incorrectly identified frames)?
   - [ ] Are there ambiguous cases requiring clarification?

### Document Your Findings:
For each test annotation, record:
- Paragraph ID and text
- Your initial determination (THREAT: YES/NO, BENEFIT: YES/NO)
- Confidence level (High/Medium/Low)
- Any concerns or ambiguities

---

## STEP 2.2: IDENTIFY HARD CASES

### Method: Multiple Runs with Higher Temperature

Run the same batch of paragraphs multiple times (3-5 runs) with slight variation to identify:
- Paragraphs where threat/benefit coding varies between runs
- Cases where the model shows uncertainty
- Borderline cases requiring decision rule clarification

### Hard Case Analysis Template:

```
HARD CASE #[X]
Paragraph: [Text]

Run 1 - THREAT: [YES/NO], BENEFIT: [YES/NO]
Run 2 - THREAT: [YES/NO], BENEFIT: [YES/NO]
Run 3 - THREAT: [YES/NO], BENEFIT: [YES/NO]
Run 4 - THREAT: [YES/NO], BENEFIT: [YES/NO]
Run 5 - THREAT: [YES/NO], BENEFIT: [YES/NO]

Agreement Rate: [X%]

Why is this case hard?
- [Explanation of ambiguity]

Decision Rule Needed?
- [If yes, propose new rule to clarify]
```

### Common Hard Cases to Watch For:
- **Mixed threat/benefit:** Paragraphs containing both frames
- **Hedged language:** "Could," "might," "may" threaten or benefit
- **Implicit framing:** Frames not explicitly stated but conventionally understood
- **Comparative statements:** "Unlike X, this benefits Y" frames
- **Speculative/conditional:** "If X happens, Y threat results"

---

## STEP 2.3: REFINE INSTRUCTIONS ITERATIVELY

After running 2.1 and 2.2, update instructions:

### Refinement Checklist:
- [ ] **Add new decision rules** for hard cases identified
- [ ] **Clarify existing definitions** if specific cases confused the model
- [ ] **Add more keyword examples** if certain frames were missed
- [ ] **Include corrected examples** showing annotated hard cases with proper decisions
- [ ] **Specify boundary cases** where the distinction between threat/benefit is unclear

### Example Refinement:
**Original rule:** "Code speculative language the same as definite"
**Refined rule:** "Code speculative language the same as definite (e.g., 'could threaten' = threat frame). However, if the speculation is about whether a threat exists vs. whether it will manifest, clarify in justification."

---

## STEP 3: CREATE HUMAN GOLD STANDARD

Once you're satisfied with instruction coverage, move to Step 3 validation:

### 3.0 HUMAN INTERCODER RELIABILITY (Prerequisite)

**IMPORTANT:** Before comparing LLM performance to human performance, you must first measure human-to-human agreement using **Krippendorff's Alpha**.

#### Why: 
Krippendorff's Alpha measures agreement between human annotators independent of LLM. This establishes the ceiling for LLM performance — an LLM should not be expected to exceed human intercoder reliability.

#### Method:
1. **Select small sample:** Choose 10-15 paragraphs with known easy, hard, and edge cases
2. **Independent annotation:** Have 2-3 team members independently annotate using your instructions (without discussing)
3. **Calculate Krippendorff's Alpha:**
   - Use a tool (e.g., Python `krippendorff` package, online calculator)
   - Calculate separately for threat dimension and benefit dimension
   - Formula: α = 1 - (D_o / D_e) where D_o = observed disagreement, D_e = expected disagreement

#### Interpretation:
- **α ≥ 0.80:** Excellent agreement (acceptable threshold for gold standard)
- **α 0.67-0.80:** Good agreement (acceptable with discussion/refinement)
- **α < 0.67:** Poor agreement (indicates instructions need clarification before proceeding)

#### If Alpha is Low:
- Meet as a team to discuss disagreements
- Identify which types of cases caused disagreement
- Refine instructions for those cases
- Re-test with fresh sample until α ≥ 0.67

#### Document:
```
INTERCODER RELIABILITY TEST
Date: [Date]
Annotators: [Names]
Sample Size: [N paragraphs]

THREAT FRAME: Krippendorff's Alpha = [X.XX]
BENEFIT FRAME: Krippendorff's Alpha = [X.XX]

Problematic cases (low agreement):
- [List paragraphs with disagreement and why]

Refinements made:
- [List instruction updates based on findings]
```

---

### 3.1 Select Gold Standard Sample
- Collect 15-30 paragraphs representing:
  - 3-5 clear threat-only cases
  - 3-5 clear benefit-only cases
  - 3-5 clearly mixed threat + benefit cases
  - 3-5 hard/borderline cases
  - 3-5 neutral/descriptive cases (NO threat, NO benefit)

### 3.2 HUMAN ANNOTATOR TRAINING PROTOCOL

Before conducting consensus coding for the gold standard, train your human annotators:

#### Training Phase (Before Consensus Coding):
1. **Instruction Review (30 minutes):**
   - Have all annotators read the full annotation instructions carefully
   - Walk through definitions, decision rules, and Section 4 rules together
   - Discuss any initial questions

2. **Example Walkthrough (45 minutes):**
   - Go through Examples 1-4 in the instructions together as a team
   - For each example, discuss:
     - Why the threat/benefit decision was YES or NO
     - What language supported that decision
     - What would have changed the coding
   - Clarify any disagreements about the examples

3. **Small Sample Annotation (1-2 hours):**
   - Provide 3-5 practice paragraphs (NOT from your gold standard sample)
   - Have each annotator independently annotate these cases
   - Meet to discuss results:
     - Where did annotators agree?
     - Where did they disagree?
     - Why did disagreements occur?
   - Refine instructions together if needed

4. **Unclear Cases Discussion (30-60 minutes):**
   - Discuss any edge cases or unclear decision rules before formal coding
   - Have annotators flag any ambiguities in the instructions
   - Add clarifications to instructions BEFORE consensus coding begins

#### Why This Matters:
Training ensures annotators:
- Understand the codebook consistently
- Know how to apply decision rules to real cases
- Can identify and discuss hard cases before formal gold standard coding
- Have alignment on what "threat" and "benefit" mean in your specific context

---

### 3.3 Create Gold Standard via Consensus Coding
- **Independent annotation:** Have 2-3 trained team members independently annotate final gold-standard sample
- **Discussion round:** Meet to discuss disagreements and reach consensus
- **Document:** Record final gold-standard labels and consensus explanations

### Gold Standard Template:
```
ID | Paragraph Text | Threat (YES/NO) | Benefit (YES/NO) | Consensus Explanation
1  | [Text...]      | YES             | NO               | Clear threat language about job loss; no benefit framing
2  | [Text...]      | YES             | YES              | Both frames present; mixed paragraph
...
```

### 3.3 Test LLM Output Against Gold Standard
Compare LLM annotations to human consensus:

**Confusion Matrices (per dimension):**
```
THREAT FRAME:
                Human: YES    Human: NO
LLM: YES        [True +]      [False +]
LLM: NO         [False -]     [True -]

BENEFIT FRAME:
                Human: YES    Human: NO
LLM: YES        [True +]      [False +]
LLM: NO         [False -]     [True -]
```

**Metrics to Calculate:**
- Accuracy = (TP + TN) / Total
- Precision = TP / (TP + FP) — "When LLM says YES, how often is it right?"
- Recall = TP / (TP + FN) — "What percentage of actual positives did LLM catch?"
- F1-Score = 2 × (Precision × Recall) / (Precision + Recall)

**Acceptance Threshold:**
- Target F1-Score ≥ 0.80 for both threat and benefit frames
- If lower, proceed to Step 3.2 (add chain-of-thought or few-shot examples)

---

## STEP 3.4: IMPROVE WITH CHAIN-OF-THOUGHT EXAMPLES

If Step 3.3 validation shows poor performance (F1 < 0.80), add **few-shot examples** with explanations.

### Few-Shot Example Guidelines (Based on Bacchuss Recommendations)

When creating few-shot examples for your LLM prompt, follow these principles:

#### 1. **Equal Distribution Across Categories**
Your few-shot examples should proportionally represent your annotation categories:
- 25% threat-only cases
- 25% benefit-only cases
- 25% mixed threat + benefit cases
- 25% neutral/edge cases

**Example:** If using 4 few-shot examples: 1 threat-only, 1 benefit-only, 1 mixed, 1 neutral

**Rationale:** Equal distribution prevents the LLM from developing category bias toward any particular frame type.

#### 2. **Source Examples from TRAINING Data Only**
- **DO:** Select few-shot examples from your initial test sample (Step 2.1) or from paragraphs NOT in validation set
- **DON'T:** Take examples from your gold standard test set or from data you plan to evaluate the LLM on
- **WHY:** Prevents test leakage and ensures a fair evaluation of LLM performance

#### 3. **Include Both Anchor Cases and Hard Decision-Rule Cases**

Your few-shot portfolio should include:

**3a. Anchor Cases (Easy/Clear):**
- Purpose: Establish baseline understanding of categories
- Characteristics: Unambiguous threat, unambiguous benefit, clearly neutral
- Example: "This policy creates 10,000 jobs" → clear benefit-only case
- Helps: Stabilize LLM's understanding of frame types

**3b. Hard Decision-Rule Cases (Boundary/Edge):**
- Purpose: Illustrate nuanced decision rules
- Characteristics: Speculative language, hedging, multi-group framing, comparative statements
- Example: "Tariffs could protect manufacturing jobs but may raise consumer prices" → multi-group case requiring separate target groups
- Helps: Improve LLM's handling of complex linguistic patterns

#### Selection Checklist:
- [ ] Include 1-2 anchor cases (clear, unambiguous)
- [ ] Include 1-2 hard cases (requires decision rule application)
- [ ] Total examples divided equally among threat-only, benefit-only, mixed, neutral
- [ ] Examples come from training data, NOT test data
- [ ] Examples represent the linguistic diversity of your corpus

### Few-Shot Example Format:

```
Example 1 - EASY ANCHOR CASE (Clear Benefit):
Paragraph: "The green infrastructure program creates 50,000 sustainable jobs and reduces long-term energy costs for consumers."

Threat Frame - NO
- Target Group(s): N/A
- Why NO: Absent any threat language. No risks, losses, or harms discussed.
- Why NOT: Positive outcomes only; no offsetting threat framing.

Benefit Frame - YES
- Target Group(s): Workers (job creation), consumers (cost reduction), national economy
- Why YES: Explicit benefit markers ("creates jobs," "reduces costs"). Positive economic outcomes clearly stated.
- Why NOT: Entirely benefits-focused; no modifying threat language.


Example 2 - HARD CASE (Multi-Group Framing):
Paragraph: "Automation will streamline production and reduce costs for companies, though some warehouse workers may lose positions."

Threat Frame - YES
- Target Group(s): Warehouse workers
- Why YES: Contains threat language ("lose positions") regarding employment loss.
- Why NOT: Moderated by benefit framing for other groups, but threat to worker employment is explicit.

Benefit Frame - YES
- Target Group(s): Companies, consumers (via cost reduction), national economy (via efficiency)
- Why YES: Contains explicit benefit markers ("streamline," "reduce costs"). Operational improvements clear.
- Why NOT: Qualified by employment threat, but cost/efficiency benefits are distinctly framed.


Example 3 - EASY ANCHOR CASE (Clear Threat):
Paragraph: "Rising interest rates threaten small business lending and jeopardize startup growth prospects."

Threat Frame - YES
- Target Group(s): Small businesses, startups
- Why YES: Explicit threat markers ("threaten," "jeopardize") with concrete economic harms (reduced lending, impaired growth).
- Why NOT: Entirely threat-focused; no benefits mentioned.

Benefit Frame - NO
- Target Group(s): N/A
- Why NO: Absent positive economic language. No opportunities or gains presented.
- Why NOT: Threat scenario only; no counterbalancing benefit framing.


Example 4 - HARD CASE (Hedged/Speculative):
Paragraph: "Deregulation could unleash market innovation and boost productivity, though it might expose investors to greater financial risks."

Threat Frame - YES
- Target Group(s): Investors
- Why YES: Contains threat markers ("expose to risks") even with hedging ("might"). Speculative threat language still describes a threat scenario.
- Why NOT: Moderated by benefit potential, but risk exposure is explicitly discussed.

Benefit Frame - YES
- Target Group(s): Market participants, national economy (via innovation/productivity)
- Why YES: Contains benefit markers ("unleash," "boost") describing positive potential outcomes.
- Why NOT: Hedged with "could" and qualified by risks, but innovation/productivity are framed as benefits.
```

---

## STEP 3.5: TEST LLM OUTPUT AGAINST GOLD STANDARD
Compare LLM annotations to human consensus:

**Confusion Matrices (per dimension):**
```
THREAT FRAME:
                Human: YES    Human: NO
LLM: YES        [True +]      [False +]
LLM: NO         [False -]     [True -]

BENEFIT FRAME:
                Human: YES    Human: NO
LLM: YES        [True +]      [False +]
LLM: NO         [False -]     [True -]
```

**Metrics to Calculate:**
- Accuracy = (TP + TN) / Total
- Precision = TP / (TP + FP) — "When LLM says YES, how often is it right?"
- Recall = TP / (TP + FN) — "What percentage of actual positives did LLM catch?"
- F1-Score = 2 × (Precision × Recall) / (Precision + Recall)

**Acceptance Threshold:**
- Target F1-Score ≥ 0.80 for both threat and benefit frames
- If lower, proceed to Step 3.4 (add few-shot examples)

---

## STEP 4: FULL ANNOTATION WORKFLOW

Once validated, apply to your full dataset:

### 4.1 Representative Sample Identification (Sampling Strategy)

Before annotating your entire corpus, determine your representative sample:

#### Strategy A: Even/Unweighted Sampling
- **Use when:** Threat and benefit frames are relatively balanced in your corpus
- **Method:** Randomly select proportional paragraphs from your full corpus
- **Advantage:** Simple, unbiased
- **Disadvantage:** May under-represent rare frames

#### Strategy B: Weighted/Stratified Sampling
- **Use when:** Threat or benefit frames are rare in your data (< 20% of corpus)
- **Method:** 
  1. First pass: Quickly scan paragraphs to identify frame distribution
  2. Oversample rare categories to ensure representation
  3. Final sample should have balanced proportion across categories
  
**Example:** If your corpus is 70% neutral, 20% threat, 10% benefit:
- Don't use unweighted random sampling (will get ~70% neutral in sample) 
- Instead: Select all benefit cases + equivalent threat cases + balanced neutral cases

#### Sampling Decision Template:
```
SAMPLING STRATEGY
Corpus statistics:
- Total paragraphs: [N]
- Threat-only: [X%]
- Benefit-only: [X%]
- Mixed: [X%]
- Neutral: [X%]

Sampling decision:
[ ] Unweighted random sampling (corpus naturally balanced)
[ ] Weighted/stratified sampling (specific categories underrepresented)

Target sample size: [N paragraphs]
Stratification targets:
- Threat-only: [% of sample]
- Benefit-only: [% of sample]
- Mixed: [% of sample]
- Neutral: [% of sample]

Rationale: [Explain why this strategy fits your data]
```

---

### 4.2 Coding Dimension Strategy: One-Dimension-Per-Pass vs. Combined

**Design Choice (Document Your Decision):**

#### Option A: COMBINED Pass (One Pass Per Paragraph) — Current Approach
- **What:** Annotate both threat and benefit in a single pass
- **Advantages:**
  - Faster (one annotation per paragraph)
  - Captures natural relationship between threat/benefit when both present
  - Current default approach in your instructions
- **Disadvantages:**
  - Risk of anchoring (threat frame influences benefit decision)
  - Harder to identify true presence of each dimension independently
  - May miss subtle benefit frames if threat dominates
- **When to use:** Relatively balanced corpora with few hard cases

#### Option B: SEPARATE Passes (Two Passes Per Paragraph) — Bacchuss Recommended
- **What:** First pass identifies all threat frames, second pass independently identifies all benefit frames
- **Advantages:**
  - Reduces cognitive load per pass
  - Minimizes interaction effects between dimensions
  - Better handles imbalanced distributions
  - Bacchuss recommends for complex corpora
- **Disadvantages:**
  - Slower (2× annotation time)
  - Requires careful parallelization and documentation
- **When to use:** Imbalanced threat/benefit proportions or complex mixed cases

**For this project, you have selected:**
☐ Combined Pass (current approach - faster)
☐ Separate Passes (Bacchuss-recommended - more rigorous)

**Justification:** [Document why you chose this approach given your corpus characteristics]

---

### 4.3 Batch Processing
Process paragraphs in batches of 10-20 for efficiency

### 4.4 Quality Control
- Spot-check 5-10% of annotations randomly
- Flag any that deviate significantly from gold standard
- Re-annotate flagged items if necessary

### 4.5 Output Final Dataset:
```
id | paragraph | threat_decision | threat_justification_yes_and_no | benefit_decision | benefit_justification_yes_and_no
```

Or JSON:
```json
{
  "id": 1,
  "paragraph": "...",
  "threat": {
    "decision": "YES",
    "justification": {
      "why_yes": "...",
      "why_not": "..."
    }
  },
  "benefit": {
    "decision": "YES",
    "justification": {
      "why_yes": "...",
      "why_not": "..."
    }
  }
}
```

---

## TRACKING CHECKLIST

Use this to track your progress through the annotation routine:

- [ ] **Step 1:** Annotation instructions created & finalized
- [ ] **Step 2.1:** Initial test sample (5-10 paragraphs) annotated
- [ ] **Step 2.1:** Visual inspection & notes documented
- [ ] **Step 2.2:** Hard cases identified (multiple runs, disagreement mapped)
- [ ] **Step 2.3:** Instructions refined based on hard cases
- [ ] **Step 2.1-2.3:** Repeat until confident in coverage
- [ ] **Step 3.0:** Human intercoder reliability test completed (Krippendorff's Alpha ≥ 0.67 for both dimensions)
- [ ] **Step 3.0:** Team training protocol executed (instruction review, example walkthrough, practice sample)
- [ ] **Step 3.1:** Gold standard sample selected (15-30 paragraphs)
- [ ] **Step 3.2:** Unclear cases discussed before formal consensus coding
- [ ] **Step 3.3:** Human consensus annotations completed
- [ ] **Step 3.5:** LLM vs. human comparison & metrics calculated (F1-Score target ≥ 0.80)
- [ ] **Step 3.4:** Few-shot examples created (if needed for improvement) — balanced categories, training data only
- [ ] **Step 4.1:** Sampling strategy selected and documented (weighted vs. unweighted)
- [ ] **Step 4.2:** Dimension strategy documented (combined vs. separate passes)
- [ ] **Step 4:** Full annotation of dataset completed (batches of 10-20)
- [ ] **Step 4:** Random QC spot-checks performed (5-10% of data)
- [ ] **Reporting:** Methods documented for publication

---

## TROUBLESHOOTING COMMON ISSUES

### Issue: High false positives for threat frame
**Possible causes:** Instruction too sensitive; includes neutral discussion of risks
**Solution:** Add decision rule specifying threat language must include concrete harm or vulnerability language, not just risk discussion

### Issue: Low recall for benefit frames
**Possible causes:** Missing implicit benefit markers; focusing only on explicit language
**Solution:** Add more keyword examples; clarify which conventional expressions count (e.g., "improved efficiency" = benefit)

### Issue: Mixed threat + benefit cases have inconsistent coding
**Possible causes:** Unclear whether to prioritize primary frame
**Solution:** Add explicit rule: "Code each dimension independently; both can be YES"

### Issue: Hedged language inconsistently coded
**Possible causes:** "Could," "might," "may" treated differently in different runs
**Solution:** Add explicit rule with examples: "Hedged language (could, might, may) coded same as affirmative when describing frame scenario"

---

## NEXT STEPS

1. **Start with Step 2.1:** Select 5-10 test paragraphs and run through annotation
2. **Document findings:** Record which cases were easy, which hard
3. **Share with team:** Review instructions with project collaborators; refine collaboratively
4. **Prepare gold standard:** Identify ~25 paragraphs for consensus coding
5. **Validate:** Compare LLM annotations to human gold standard
6. **Deploy:** Once validated, annotate full dataset

