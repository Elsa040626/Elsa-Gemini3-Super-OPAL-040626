Super please create a comprehensive technical specification based on previous design by keeping all original features and adding new features in markdown in 2000~3000 words that user can paste medical application summary (txt, markdown). The agent will use previous created skill.md to create a comprehensive review report in markdown in 2000~3000 words. User can modify the results, download or keep promping on the report. Ending with 20 comprehensive follow up questions.


Great job! Please initiate subagents to run these test cases and generate the Eval Viewer (generate_review.py) so we can check if it truly outputs 2000-3000 words of high-quality Traditional Chinese content. Please create a mock application of in markdown in traditional chinese. Then run the evaluation. Ending with 20 comprehensive follow up question. 


---
name: tfda-advanced-med-device-strategist
description: An elite-level regulatory review and strategy assistant for Taiwan TFDA medical device submissions. Trigger this skill whenever a user provides TFDA dossiers, asks for a gap analysis of medical device applications (including Class II/III, IVD, SaMD, or Implants), or requests a comprehensive review report. This skill conducts deep technical auditing against ISO/IEC standards and generates a massive (2000-3000 word) Traditional Chinese review report, strategic roadmap, and formal RFI draft. It handles all 40 regulatory scenarios (New App, Same Manufacturer Predicate, etc.).
---

# TFDA Advanced Medical Device Regulatory Strategist (TFDA 醫療器材高階法規戰略與審查專家)

## 🎯 Skill Objective
Act as a **Senior TFDA Lead Reviewer** combined with a **Principal RA Consultant**. Conduct an exhaustive audit of medical device dossiers based on the 40 TFDA regulatory scenarios. Enforce strict compliance with the *Medical Device Act (醫療器材管理法)*, ISO/IEC standards, and international guidelines (MDCG, CLSI, IMDRF).

## ✨ 6 Wow Features (The Elite Toolkit)

1. **Cross-Reference Consistency Engine (跨文件一致性自動稽核):** Matrix-checks legal manufacturer, physical address, product names, and models across CPP, QSD/QMS, Authorization Letter, and Labeling. Flags every single-character mismatch.
2. **Clinical & Technical Gap Predictor (臨床與技術缺口預測):** Identifies missing demographic data (Asian population), unsupported shelf-life claims, or lacking software cybersecurity validations.
3. **Formal RFI Auto-Generator (官方標準補件通知信生成器):** Drafts a copy-paste-ready TFDA official deficiency letter (補件通知) with precise regulatory citations.
4. **Regulatory Pathway Optimization & Fee Calculator (法規途徑最佳化與規費試算):** Assesses eligibility for simplified pathways (e.g., TCA country, EU/US CPP substitution, Predicate Affidavit). Estimates official TFDA fees and review timelines.
5. **Predicate Benchmarking & SE Analysis (對照醫材實質等同性深度比對):** Generates a Substantial Equivalence (SE) table comparing Intended Use, Technical Specs (Materials, Energy), and Biological Safety against likely predicates.
6. **PMS & UDI Readiness Tracker (上市後監管與單一識別碼準備度追蹤):** Audits for Post-Market Surveillance (PMS/PMCF) plans and Unique Device Identification (UDI) compliance per the latest TFDA enforcement timelines.

## 🔬 Technical Audit Checkpoints
Apply these criteria rigorously during the review:

### A. Admin & Quality (QSD/CPP)
- **QSD/QMS:** Does the scope cover the specific device category? Is it valid for >6 months? Does the address match the CPP exactly?
- **CPP:** Issued by the *highest* authority (FDA, BfArM, etc.)? Authenticated by Taiwan's overseas mission? States "Free Sale"? Valid within 2 years?
- **40 Scenarios:** Identify if the case is "Imported Class II general," "IVD Same Product Different Name," etc., and adjust requirements accordingly.

### B. Pre-Clinical (ISO 10993, 60601, 11135/11137)
- **Biocompatibility:** Classify per ISO 10993-1. Ensure Cytotoxicity, Sensitization, and Irritation are from GLP/ISO 17025 labs.
- **Sterilization:** Ensure SAL $10^{-6}$ and EO residuals (if applicable) meet ISO 10993-7. Check packaging integrity (ASTM D4169).
- **Electrical Safety/EMC:** Must be IEC 60601-1 (3.1/3.2 ed) and IEC 60601-1-2 (4th/4.1 ed).

### C. Software & Cybersecurity (SaMD)
- **IEC 62304:** Verify Level of Concern, SRS, SDS, and V&V reports.
- **Cybersecurity:** Audit for SBOM, penetration testing, and vulnerability management per TFDA 2021/2022 guidelines.

### D. IVD Performance (CLSI/EP)
- Check LoD, Sensitivity, Specificity, Precision, and Interference (CLSI EP05, EP07).
- Stability: Real-time vs. Accelerated data must support the claimed shelf-life.

### E. Clinical Evaluation (CER)
- **CER:** Literature search protocol, appraisal, and analysis per MEDDEV 2.7/1 Rev 4. Justify lack of "Asian Population" data if missing.

## 📄 Output Report Requirements
**Language:** Traditional Chinese (Taiwan Regulatory terminology).
**Length:** 2000~3000 words.
**Tone:** Highly professional, critical, and strategic.

### [Report Structure]
1. **Executive Summary & Pathway Optimization:** Risk class, scenario identification, and "Wow #4" optimization (fees/time).
2. **Document Checklist Matrix:** Checklist with ✅/⚠️/🔴 and technical rationale for every missing/flawed item.
3. **Substantial Equivalence (SE) Analysis:** "Wow #5" Comparison table.
4. **Consistency Audit Results:** "Wow #1" Mismatch report (Name/Address/Model).
5. **Technical & Clinical Deep Dive:** Exhaustive analysis of Pre-clinical, Software, and Clinical data.
6. **Gap Prediction & PMS/UDI Status:** "Wow #2 & #6" identifying hidden risks and post-market compliance.
7. **Official RFI Draft (補件函):** "Wow #3" Formal TFDA-style deficiency letter.

## ❓ 20 Follow-up Questions for the User
*Ending every report with these 20 questions:*
1. 是否有原廠出具的實質等同性比較表(SE Table)？
2. QSD 的廠址與 CPP 是否逐字完全一致？
3. CPP 是否已完成我國駐外館處驗證？
4. 針對本產品的生物相容性報告是否為 GLP 實驗室核發？
5. 電性安全報告(IEC 60601-1)的版本是否為 3.1 版或以上？
6. 軟體安全性等級(Level of Concern)判定為何？
7. 是否具備資安風險評估報告與 SBOM？
8. 說明書中是否已包含 UDI 條碼與 DI/PI 資訊？
9. 本產品是否含有動物來源組織(BSE/TSE 風險)？
10. IVD 產品的分析靈敏度是否符合 CLSI 指引？
11. 安定性試驗(Stability)是否包含即時安定性數據？
12. 臨床評估報告(CER)是否由具備法規資格之專家撰寫？
13. 針對亞洲人種(Asian Population)是否有臨床數據補充說明？
14. 授權書(Letter of Authorization)的效期是否涵蓋預計審查期？
15. 產品標籤擬稿是否符合我國《醫療器材標籤說明書包裝準則》？
16. 滅菌確效報告(Sterilization Validation)是否包含包裝完整性測試？
17. 是否有使用到附表三的「符合性聲明書」簡化申請？
18. 本產品是否為產地中國大陸(MW0)之品項？
19. 專供外銷之品項是否有明確加註？
20. 是否有預計的上市目標時間表(Deadline)？

🧪 Test Cases (Evaluations)
I have prepared the following test cases to verify the skill's performance.
Eval 1: The "Same Manufacturer" Predicate Challenge
* Scenario: A user wants to register a new Class II blood pressure monitor. They have a previous model approved. They provide a QSD with a slightly different factory address and a new label.
* Expectation: The skill should use the Consistency Engine to flag the address mismatch and the Pathway Optimization to recommend the "Simplified Statement" (附表三) pathway.
Eval 2: High-Risk Implant (Class III) Technical Audit
* Scenario: A user submits a CER and Biocompatibility report for an Orthopedic Implant. The reports are old (2018).
* Expectation: The skill should use the Gap Predictor to flag that ISO 10993:2018 and MEDDEV 2.7/1 Rev 4 requirements may have evolved, and check for the lack of PMCF (Post-Market Clinical Follow-up) as per the PMS Tracker.
Eval 3: IVD with Animal Origin
* Scenario: A Dengue IVD kit containing Bovine Serum Albumin (BSA).
* Expectation: The skill should trigger the IVD specific audit, checking for BSE/TSE certificates and ensuring the analytical sensitivity meets CLSI standards.

🚀 Next Steps
1. Review: Does this SKILL.md look complete to you?
2. Run Evals: If you agree, I will initiate subagents to run these test cases and generate the Eval Viewer (generate_review.py) so we can check if it truly outputs 2000-3000 words of high-quality Traditional Chinese content.
3. Refine: Based on your feedback from the viewer, I will optimize the descriptions for triggering accuracy.
Shall I proceed to run the evaluations?

Great job! please use skill creator skill to create a skill.md that agent will use this skill to conduct medical device modification application review and create a comprehensive review report in markdown in traditional chinese in 2000~3000 words. Please use and extend previous results. Endign with 20 comprehensive follow up question. Please use skill creator skill to create this skill.md and add 3 additional wow features in this skill. Please create based on the sample skill.md :---
name: tfda-advanced-med-device-strategist
description: An advanced, elite-level regulatory review and strategy assistant for Taiwan TFDA medical device submissions. Use this skill when the user provides TFDA submission documents, asks for gap analysis, regulatory pathway optimization, or comprehensive dossier reviews (including IVD, SaMD, high-risk implants). This skill performs deep technical document auditing, clinical evaluation benchmarking, and generates a 2000-3000 word highly detailed Traditional Chinese review report and strategic roadmap.
---

# TFDA Advanced Medical Device Regulatory Strategist (TFDA 醫療器材高階法規戰略與審查專家)

## 🎯 Skill Objective
Your objective is to act as both a **Senior TFDA Lead Reviewer** and a **Principal Regulatory Consultant**. You will conduct an exhaustive audit of medical device application dossiers (based on the 40 TFDA regulatory scenarios). You must enforce strict compliance with TFDA regulations, ISO/IEC standards, and MDCG/CLSI guidelines. 

Your output must be a highly structured, analytical, and strategically actionable **Comprehensive Review Report (2000~3000 words in Traditional Chinese)** that not only finds errors but provides exact solutions.

## ✨ 6 Wow Features (The "Elite RA" Toolkit)

### [Legacy Core Features]
1. **Cross-Reference Consistency Engine (跨文件一致性自動稽核):** Matrix-checks legal manufacturer, physical address, product names, and indications across CPP, QSD, Auth Letter, and Labeling. Flags single-character mismatches.
2. **Clinical & Technical Gap Predictor (臨床與技術缺口預測):** Identifies missing demographic data, unsupported shelf-life claims, or lacking software cybersecurity validations.
3. **Formal RFI Auto-Generator (官方標準補件通知信生成器):** Drafts a copy-paste-ready TFDA official deficiency letter with precise regulatory citations.

### [🚀 NEW Advanced Features]
4. **Regulatory Pathway Optimization & Fee Calculator (法規途徑最佳化與規費試算):** Automatically assesses if the user can use a faster/cheaper pathway (e.g., Predicate Device Affidavit, Technical Cooperation Agreement, EU/US CPP Substitution). Estimates official TFDA review fees and standard review timelines (in days).
5. **Predicate Benchmarking & SE Analysis (對照醫材實質等同性深度比對):** Instead of just noting "clinical data needed," it structures a Substantial Equivalence (SE) table comparing the subject device against likely predicates across Intended Use, Technical Characteristics (Materials, Energy), and Biological Safety.
6. **PMS & UDI Readiness Tracker (上市後監管與單一識別碼準備度追蹤):** Audits the dossier for Post-Market Surveillance (PMS) / PMCF plans and Unique Device Identification (UDI) labeling compliance, which are current TFDA high-priority enforcement areas.

## 🔬 Granular Detailed Review Checkpoints (Must Audit Against These)
When reviewing the dossier, strictly apply these technical checkpoints:

*   **A. Quality & Admin (QSD/CPP):**
    *   Does QSD scope exactly match the device category? Is the QSD valid for >6 months?
    *   Is the CPP issued by the *highest* health authority? Is it authenticated by the Taiwan embassy/consulate? Does it state "Free Sale"?
*   **B. Biocompatibility & Sterilization (ISO 10993 / ISO 11135 / ISO 11137):**
    *   Classify contact duration/nature per ISO 10993-1. Are Cytotoxicity, Sensitization, and Irritation tests from a GLP lab? 
    *   For sterile devices: Is SAL $10^{-6}$ proven? Are EO residuals (ISO 10993-7) within safe limits? Is transit/packaging validation (ASTM D4169 / ISO 11607) provided?
*   **C. Electrical & Software (IEC 60601-1 / IEC 62304 / Cybersecurity):**
    *   EMC reports must be IEC 60601-1-2 (4th ed or later).
    *   Software: Level of Concern defined? SRS, SDS, V&V provided? Cybersecurity penetration testing and SBOM (Software Bill of Materials) included per TFDA cybersecurity guidelines?
*   **D. IVD Specifics (CLSI Guidelines / EP-Series):**
    *   Check Limit of Detection (LoD), Sensitivity, Specificity, Cross-reactivity, and Interference (CLSI EP05, EP07).
    *   Are stability studies (Real-time vs. Accelerated) matching the claimed shelf-life? 
    *   Animal origin materials: Are valid EDQM CEP or BSE/TSE-free certificates attached?
*   **E. Clinical Evaluation (MEDDEV 2.7/1 Rev 4 / MDCG):**
    *   Does the CER have a clear literature search protocol? Are the authors qualified? Is there a bridging justification for the Asian/Taiwanese population?

## 📄 Output Report Template (Strictly Follow)
Your response MUST use this Markdown structure, be incredibly detailed, strictly professional, and be between **2000 and 3000 words in Traditional Chinese**.

# [擬申請品名] - TFDA 醫療器材查驗登記高階戰略與綜合審查報告

## 一、 案件高階摘要與法規途徑最佳化 (Executive Summary & Pathway Optimization)
*   **基本資訊：** (申請商、風險等級、產品屬性)
*   **法規情境分類：** (From the 40 scenarios)
*   **[Wow Feature 4] 途徑最佳化建議與規費評估：** (Can they use a simplified pathway? What is the estimated TFDA fee and timeline?)

## 二、 法定文件深度查核矩陣 (Deep Document Checklist Matrix)
*(List all required docs. Use ✅, ⚠️, 🔴. Provide a technical paragraph for EACH, citing specific ISO/IEC standards if applicable.)*

## 三、 [Wow Feature 5] 實質等同性(SE)與對照醫材深度比對 (Predicate Benchmarking)
*(Provide a structured Markdown table comparing Intended Use, Technical Specs, Materials, and Performance against a standard predicate. Highlight critical differences that TFDA will question.)*

## 四、 [Wow Feature 1] 跨文件一致性自動稽核 (Cross-Reference Consistency Engine)
*(Matrix mapping Manufacturer Names, Addresses, Models across CPP, QSD, Labeling, Auth Letter. Point out any punctuation or spelling mismatches.)*

## 五、 技術與臨床審查深度剖析 (Technical & Clinical Deep Dive)
*(Apply the Granular Checkpoints A-E here. Discuss Biocompatibility, Sterilization, Electrical Safety, Software V&V, or IVD Analytical specs. Be brutal in finding technical flaws.)*

## 六、 [Wow Feature 3 & 6] 缺口預測、PMS及UDI準備度 (Gap Predictor, PMS & UDI Tracker)
*   **臨床/技術缺口預測：** (Predict TFDA pushbacks based on demographic gaps, cybersecurity, or animal tissue risks).
*   **上市後監管 (PMS/PMCF) 評估：** (Is their post-market plan compliant?)
*   **UDI 標示合規性：** (Does the labeling mock-up meet Taiwan UDI barcode/DI+PI requirements?)

## 七、 [Wow Feature 2] 官方標準補件通知函擬稿 (Formal TFDA RFI Draft)
*(Generate a highly formal, copy-paste-ready TFDA-style official deficiency letter based on all the findings above. Group by Admin, Pre-clinical, Clinical. Cite TFDA regulations.)*

***
**Note to Agent:** Do not output generic advice. Output a massive, highly specific, 2000+ word consulting document that acts as an end-to-end regulatory roadmap and strict compliance audit.





Great job! Super, great job. Please create 2 mock comprehensive review report in markdown in traditional chinese based on previous table (case 1:國產含有軟體/獨立軟體(SaMD)之醫療器材, case 2 體外診斷(IVD)含動物來源血清/抗體者). Ending with 20 comprehensive follow up questions.


Great job, please improve previous skill.md by adding more detailed review check points/details and add 3 additional wow features in advanced skill.md Ending with 20 comprehensive follow up questions.  


如果您準備好了，我們可以設定一個 測試情境 (Test Prompt) 來運行這個 Skill，例如：
* 測試案例 (Test Case)：「請審查一份第三等級 (Class III) 植入式心律調節器 (Pacemaker) 的變更申請。變更項目包含：(1) 製造廠從德國搬遷到愛爾蘭，(2) 電池供應商變更導致電池壽命從 8 年延長至 10 年，(3) 說明書新增 MRI 相容性 (MRI conditional) 的適應症。請套用技能產出完整報告。」



