# Link to Behavior: Economy – Threat Frames and Benefit Frames

## 📌 Project Overview

This project provides a comprehensive, research-backed annotation framework for identifying and analyzing **economic threat frames** and **economic benefit frames** in text. It implements the **bacchuss annotation routine**, a systematic methodology for developing reliable, intersubjectively valid automated text annotation.

### Purpose

This framework enables researchers, annotators, and data scientists to:
- **Identify economic threat frames** in text (risk, vulnerability, loss, crisis language)
- **Identify economic benefit frames** in text (opportunity, growth, gain, prosperity language)
- **Provide dual-sided justifications** for each determination (explain both YES and NOT)
- **Validate annotations** against human gold standards
- **Deploy reliable annotation pipelines** for large-scale text analysis

### Key Innovation

Unlike simple binary coding, this framework requires **dual-sided justification for each determination**:
- If you say **YES** to threat frame: Explain why it IS a threat frame AND why it is NOT a benefit frame
- If you say **NO** to threat frame: Explain why it is NOT a threat frame AND why it could be a benefit frame
- Same approach for benefit frames independently

This rigorous approach creates **intersubjectively valid, defensible annotations**.

---

## 🚀 Quick Start

### 1. Start Here
Read **[QUICK_START.md](QUICK_START.md)** (15 minutes)
- Get oriented with the task
- Understand the workflow
- Review key principles

### 2. Learn the Definitions
Read **[annotation_instructions_threat_benefit.md](annotation_instructions_threat_benefit.md)**
- Section 3: Definitions of threat and benefit frames
- Section 3: Keywords and markers
- Section 7: Worked examples

### 3. Try an Annotation
Use **[annotation_template.md](annotation_template.md)**
- Pick 1-2 test paragraphs
- Complete the annotation form
- Get hands-on experience

### 4. Follow the Workflow
Read **[implementation_guide.md](implementation_guide.md)**
- Step 2.1: Test initial instructions
- Step 2.2: Identify hard cases
- Step 3: Validate against human consensus
- Step 4: Deploy to full dataset

---

## 📂 Project Structure

```
├── README.md                                    # This file
├── INDEX.md                                     # File directory and quick reference
├── QUICK_START.md                               # 5-step getting started guide
├── annotation_instructions_threat_benefit.md    # Complete annotation codebook
├── annotation_template.md                       # Ready-to-use annotation forms
└── implementation_guide.md                      # Full bacchuss workflow guide
```

### File Descriptions

| File | Purpose | When to Use |
|------|---------|-----------|
| **QUICK_START.md** | Fast introduction & workflow | First - get oriented |
| **annotation_instructions_threat_benefit.md** | Detailed codebook & definitions | Reference during annotation |
| **annotation_template.md** | Annotation forms & tracking | While annotating paragraphs |
| **implementation_guide.md** | Step-by-step validation procedure | Plan workflow & quality control |
| **INDEX.md** | File index & cross-reference | Navigate between documents |

---

## 🎯 Key Concepts

### Economic Threat Frame
**Definition:** Language emphasizing negative economic outcomes, risks, losses, or vulnerability.

**Keywords:** threat, risk, danger, loss, damage, vulnerability, crisis, job loss, decline, jeopardy, recession, bankruptcy, collapse

**Example:** *"The policy threatens to eliminate 50,000 manufacturing jobs and destabilize the economy."*

### Economic Benefit Frame
**Definition:** Language emphasizing positive economic outcomes, opportunities, gains, or growth.

**Keywords:** opportunity, growth, expansion, create, gain, improve, strengthen, advantage, prosper, productivity, job creation, competitive advantage

**Example:** *"This initiative creates 10,000 new jobs and boosts overall productivity."*

### Dual-Sided Justification
For each determination, explain **both sides**:
- Why it IS/IS NOT the frame (based on language markers)
- Why it IS/IS NOT the opposite frame (addressing counterargument)

---

## 📊 Annotation Workflow

### Phase 1: Understanding (1-2 hours)
- [ ] Read definitions and examples
- [ ] Understand threat vs. benefit frames
- [ ] Review decision rules for hard cases

### Phase 2: Testing & Refinement (2-4 hours)
- [ ] Test instructions on 5-10 sample paragraphs
- [ ] Identify hard cases and ambiguities
- [ ] Refine understanding based on findings
- [ ] Repeat until coverage is broad

### Phase 3: Validation (2-4 hours)
- [ ] Build gold standard sample (15-30 paragraphs)
- [ ] Team consensus coding
- [ ] Measure reliability against human judgment
- [ ] Calculate precision, recall, F1-score

### Phase 4: Deployment (varies)
- [ ] Annotate full dataset
- [ ] QC spot-checks (5-10% random review)
- [ ] Document methodology
- [ ] Export final results

---

## 📋 Annotation Process Overview

For each paragraph:

```
1. Read paragraph carefully
   ↓
2. Identify threat language (if present)
   ↓
3. Identify benefit language (if present)
   ↓
4. Make THREAT FRAME decision (YES/NO)
   └─ Explain: Why IS it a threat? Why is it NOT a benefit?
   ↓
5. Make BENEFIT FRAME decision (YES/NO)
   └─ Explain: Why IS it a benefit? Why is it NOT a threat?
   ↓
6. Flag difficulty level
   └─ Clear / Ambiguous / Hard case
   ↓
7. Document for consistency
```

---

## 🔑 Core Principles

✅ **DO:**
- Be **literal** – Look for explicit language in text, not inference
- **Evaluate independently** – Both threat AND benefit can be YES
- **Provide dual justification** – Always explain both sides
- **Flag hard cases** – Mark ambiguous paragraphs for discussion
- **Iterate and refine** – Learn from testing phase

❌ **DON'T:**
- Infer meanings not stated in text
- Assume threat and benefit are opposites
- Skip justification requirements
- Ignore hedged language ("could," "might," "may")
- Rush through annotations

---

## ✅ Critical Template Additions Included

This project now includes the required items before practical execution:

1. **Target Group field** in definitions, template, and output format
2. **Benefit-only worked example** for balanced guidance
3. **Few-shot construction guidelines** (balanced categories, no validation leakage, easy + hard examples)
4. **Human intercoder reliability step** using Krippendorff's Alpha before LLM comparison
5. **Human annotator training protocol** before gold-standard consensus coding
6. **Sampling strategy guidance** (weighted vs unweighted) for representative validation
7. **One-dimension-per-pass design note** (combined vs separate passes, with justification)

These additions are implemented in:
- `annotation_instructions_threat_benefit.md`
- `annotation_template.md`
- `implementation_guide.md`

---

## 📈 Bacchuss Annotation Routine

This framework implements the **bacchuss annotation routine** – a systematic, research-backed methodology for developing reliable automated text annotation:

### 5-Step Procedure:
1. **Write initial annotation instructions** (codebook)
2. **Test & refine** on samples, identify problems
3. **Identify hard cases** through multiple runs
4. **Build gold standard** with human validation
5. **Deploy & report** to full dataset with full transparency

### Why This Approach?
- Creates **intersubjectively valid** annotations (defensible, documentable)
- Produces **reliable results** (high precision & recall)
- Enables **transparency** (full methodology documented)
- Supports **reproducibility** (other researchers can replicate)

---

## 💻 Usage Examples

### Example 1: Clear Threat Frame
```
Paragraph: "The proposed tariffs will destroy manufacturing jobs 
            and trigger a trade war with our largest markets."

Threat Frame: YES
- Why YES: Explicit threat language ("destroy," "war") with 
           economic harm consequences
- Why NOT: No offsetting benefit framing; no positive outcomes mentioned

Benefit Frame: NO
- Why NO: Absent any opportunity, growth, or positive language
- Why NOT: Threat framing is dominant and unambiguous
```

### Example 2: Mixed Frame (Both YES)
```
Paragraph: "Automation will displace some workers initially, but will 
            increase overall productivity and create new high-skill jobs 
            in the long term."

Threat Frame: YES
- Why YES: Job displacement explicitly mentioned ("will displace")
- Why NOT: Also frames future opportunity; mixed messaging

Benefit Frame: YES
- Why YES: Productivity gains and job creation explicitly stated
- Why NOT: Qualified by initial displacement; mixed messaging

Combination: BOTH threat AND benefit frames present
```

### Example 3: Neutral Descriptive
```
Paragraph: "The unemployment rate decreased from 5.2% to 4.8% 
            in the reported quarter."

Threat Frame: NO
- Why NO: Pure descriptive data without framing or risk language
- Why NOT: Improvement noted, but no threat scenario discussed

Benefit Frame: NO
- Why NO: Descriptive reporting without explicit benefit language
- Why NOT: While improvement is positive, active benefit framing 
           (opportunity, gain, advantage) is absent
```

---

## 🔧 For Researchers & Teams

### Single Annotator Setup
1. Follow QUICK_START.md workflow
2. Test on small sample (5-10 paragraphs)
3. Build personal gold standard if possible
4. Annotate dataset with periodic self-checks

### Team Collaboration
1. **Kickoff meeting (30 min):**
   - Review definitions & examples together
   - Discuss any clarifications needed

2. **Independent testing (1-2 hours):**
   - All team members annotate same 3-5 paragraphs
   - Document any disagreements

3. **Consensus meeting (45 min):**
   - Compare annotations
   - Discuss disagreements
   - Build shared understanding

4. **Gold standard creation (2-4 hours):**
   - Team builds 20-30 consensus-coded paragraphs
   - Measure inter-rater reliability
   - Establish quality standards

5. **Full annotation (ongoing):**
   - Individual annotators proceed with full dataset
   - Periodic team check-ins for hard cases
   - QC spot-checks

---

## 📊 Quality Metrics

### Target Performance:
- **F1-Score:** ≥ 0.80 for both threat and benefit frames
- **Precision:** Minimize false positives
- **Recall:** Minimize false negatives

### Calculation:
```
Precision = True Positives / (True Positives + False Positives)
Recall = True Positives / (True Positives + False Negatives)
F1-Score = 2 × (Precision × Recall) / (Precision + Recall)
```

See **implementation_guide.md** Section 3.1 for detailed procedures.

---

## 🤖 For LLM-Based Annotation

These instructions are LLM-ready. To use:

1. Provide the LLM with **annotation_instructions_threat_benefit.md**
2. Include relevant examples from Section 7
3. Test on small sample first
4. Refine instructions based on performance
5. Validate against human gold standard
6. Deploy if metrics acceptable

The comprehensive decision rules and examples significantly improve LLM annotation reliability.

---

## 📚 References & Further Reading

### Annotation Methodology
- Neuendorf, K. A. (2002). *The Content Analysis Guidebook*. Thousand Oaks, CA: Sage.
- Krippendorff, K. (2019). *Content Analysis: An Introduction to Its Methodology*. Thousand Oaks, CA: Sage.

### Chain-of-Thought & Few-Shot Learning
- Wei, J., et al. (2022). "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models." arXiv preprint arXiv:2201.11903.
- Brown, T., et al. (2020). "Language Models are Few-Shot Learners." NeurIPS 2020.

### Economic Framing in Communication
- Entman, R. M. (1993). "Framing: Toward Clarification of a Fractured Paradigm." *Journal of Communication*, 43(4), 51-58.
- Lakoff, G. (2010). "Why it Matters How We Frame the Environment." *Environmental Communication*, 4(1), 70-81.

---

## 👨‍💻 Getting Help

### Common Questions:
- **How do I start?** → Read QUICK_START.md
- **What counts as a threat frame?** → See annotation_instructions_threat_benefit.md Section 3.1
- **How do I handle mixed cases?** → See annotation_instructions_threat_benefit.md Section 4.1
- **How do I validate my annotations?** → See implementation_guide.md Step 3

### Troubleshooting:
See **implementation_guide.md** "Troubleshooting Common Issues" section for:
- High false positives
- Low recall
- Inconsistent mixed-frame coding
- Hard case handling

---

## 📝 Project Information

**Project Title:** Link to Behavior: Economy – Threat Frames and Benefit Frames

**Framework:** Bacchuss Annotation Routine

**Release Date:** April 2026

**Version:** 1.0

**Status:** Active - Ready for use

---

## 📄 License & Attribution

This annotation framework implements the bacchuss annotation routine. Please cite appropriately if used in research.

### Recommended Citation:
```
Annotation Framework for Economic Threat and Benefit Frames (2026). 
Link to Behavior: Economy Project.
Available at: https://github.com/123Sarthak-cyber/Grades1
```

---

## 📞 Support & Contributions

For questions, clarifications, or contributions:
1. Review all documentation thoroughly
2. Check QUICK_START.md and implementation_guide.md
3. Consult decision rules in annotation_instructions_threat_benefit.md Section 4
4. Document hard cases for team discussion

---

## 🎓 Quick Reference

**For annotations:**
- Threat frame keywords: threat, risk, danger, loss, vulnerability, crisis, job loss
- Benefit frame keywords: opportunity, growth, expand, create, improve, prosperity, advantage
- Always provide dual-sided justification
- Both threat AND benefit can be YES in same paragraph

**For workflow:**
- Phase 1: Understand definitions (1-2 hours)
- Phase 2: Test & refine (2-4 hours)
- Phase 3: Validate (2-4 hours)
- Phase 4: Deploy (varies by dataset size)

**For output:**
- Format: Paragraph text + Threat decision + Threat justification + Benefit decision + Benefit justification
- See annotation_template.md for JSON, CSV, Markdown formats

---

## 🚀 Start Now

1. **Open QUICK_START.md** → Read Section "Getting Started in 5 Steps"
2. **Pick 1-2 paragraphs** → Test your understanding
3. **Complete annotation form** → Use annotation_template.md
4. **Follow implementation_guide.md** → Phase 2 testing procedure

**You're ready to begin!**

---

*Last Updated: April 13, 2026*  
*For the latest version, visit the GitHub repository*

