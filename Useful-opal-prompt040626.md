super please extended the terchnical specification by keeping all original features (please include previous skill.md as default in the spec) and adding additional wow interactive indicator , live log, wow dashboard in markdown in 3000~4000 woeds. Endimg with 20 comprehensive follow up questions

Super please create a comprehensive technical specification based on previous design by keeping all original features and adding new features in markdown in 2000~3000 words that user can paste medical application summary (txt, markdown). The agent will use previous created skill.md to create a comprehensive review report in markdown in 2000~3000 words. User can modify the results, download or keep promping on the report. Ending with 20 comprehensive follow up questions.Agentic Medical Device Reviewer – Improved System Technical Specification (v2)
Target platform: Hugging Face Spaces (Streamlit) • Config-driven agents via agents.yaml • Multi-LLM (OpenAI, Gemini, Anthropic, Grok)

1. Purpose & Scope
This specification defines an improved design for the Agentic Medical Device Reviewer system. It preserves all original features (multi-tab Streamlit app, WOW UI themes/styles, agent pipeline execution with editable handoffs, TFDA premarket workflows, FDA 510(k) intelligence and review pipeline, PDF→Markdown conversion, Note Keeper with AI Magics, agents.yaml studio, dashboard/history) and adds new features for:

Published Guidance Ingestion + FDA/International Regulatory Research Report Generation
Users can paste or upload published guidance in TXT / Markdown / PDF.
Users select output language: Traditional Chinese (default) or English.
A research agent analyzes the provided document, searches and retrieves FDA-related information (e.g., 510(k) summaries, FDA guidance, FDA Recognized Consensus Standards), plus relevant international regulations and industry standards, then synthesizes everything into a grounded, citation-rich Markdown report (2000–3000 words).
Users can modify prompts and select models (restricted for this feature to Gemini: gemini-2.5-flash, gemini-3-flash-preview).
Users can edit results and download as .txt or .md.
2. Template-Based Report Rewriter

Users can provide a regulatory report template (paste/upload) or select a default template library (including the provided Orthopedic External Fixators guidance+checklist template).
A second agent rewrites the comprehensive report to match the chosen template, still grounded, with consistent section mapping.
Users can modify prompt/model (Gemini models above), edit outputs, and download.
3. Skill Generator (skill.md) for New Agent Skill Creation

From the final template-based report + the original guidance structure, a third agent generates a skill.md file content that defines a new agent skill in the standard skill-creator format.
Output language matches the user selection (TC/EN).
Users can modify prompt and select models (gemini-2.5-flash, gemini-3-flash-preview, gemini-3.1-flash-lite-preview).
Adds 3 “WOW” features inside the generated skill (defined in §8.3).
Additionally, the system adds 3 new “WOW AI features” across the product (beyond existing Note Keeper Magics), and upgrades the dashboard/status indicators, while maintaining the existing API key handling behavior with an enhancement: users can input keys on the webpage if environment keys are absent, and environment-provided keys are never displayed.

2. Baseline (Original) Capabilities – Must Remain Intact
2.1 UI & Experience
Streamlit multi-tab application with a “WOW UI” layer:
Light/Dark theme toggle
English / Traditional Chinese UI language
20 painter-inspired styles and a Jackpot random style picker
Global sidebar settings: default model, temperature, max tokens
Status indicators (pending/running/done/error) for agent runs
An interactive dashboard with run history and charts
2.2 LLM & Agent Orchestration
Multi-provider LLM routing:
OpenAI: gpt-4o-mini, gpt-4.1-mini
Gemini: gemini-2.5-flash, gemini-3-flash-preview, gemini-2.5-flash-lite, gemini-3.1-flash-lite-preview
Anthropic models (configurable)
Grok: grok-4-fast-reasoning, grok-3-mini
Agent definitions loaded from agents.yaml with a UI editor/studio
Sequential agent execution:
Users can edit prompt and choose model per agent
Users can edit outputs (text/markdown modes) and pass as input to the next agent
2.3 Regulatory Workflows
TFDA premarket tab:
Application import/export (JSON/CSV), completeness indicator
Guidance ingestion and pre-screening agents
Application markdown drafting and improvement
FDA 510(k) intelligence and review pipeline
PDF → Markdown conversion
Note Keeper:
Paste note → organized Markdown with highlighted keywords
User-editable note views
AI Magics (including AI Keywords with user-defined color)
2.4 Deployment & Ops
Deployed on Hugging Face Spaces using Streamlit
Uses environment variables for secrets when available; session state for runtime values
Works without code modifications through agents.yaml extensibility
3. New Capability A: Published Guidance Ingestion + Regulatory Research Report
3.1 User Goals
Upload/paste a published guidance (e.g., TFDA review guidance, internal SOP, public regulatory guidance).
Produce a credible, grounded report that:
Extracts key requirements from the input guidance
Identifies FDA-aligned pathways and evidence expectations
Cross-references FDA sources (510(k) summaries, guidance, recognized standards)
Extends to international regulations (EU MDR/IVDR as applicable, IMDRF, ISO/IEC standards, etc.)
Outputs in Traditional Chinese (default) or English
Includes citations and a research trail suitable for regulatory teams
3.2 Input Types & Ingestion Requirements
Supported inputs (single or multiple):

Paste: plain text / Markdown
Upload: .txt, .md, .pdf
Ingestion processing (design requirements):

PDF text extraction:
Page-by-page extraction with page boundary markers for traceability
Store extracted text plus metadata: filename, upload timestamp, page count, extraction warnings
Markdown/TXT normalization:
Preserve headings and lists if present
Detect encoding issues (e.g., mixed Chinese punctuation) and normalize
Document fingerprinting:
Compute a “structure signature” (e.g., heading outline + section keywords) used later for template mapping and skill creation
Language detection (non-blocking):
Detect primary language of input to guide bilingual term consistency, but output language is always user-selected
3.3 Output Language Control
Output language selector on the feature panel:
繁體中文 (default)
English
The selection must propagate to:
Prompts (system/user)
Report headings and table labels
Generated skill.md language
4. New Capability B: FDA + International Research (Search & Grounding)
4.1 Research Sources (Target Corpus)
The research agent must prioritize official and reputable sources:

FDA-related (required emphasis):

FDA Guidance documents (device-specific and general)
FDA Recognized Consensus Standards database
FDA 510(k) database:
510(k) summaries (when publicly available)
device classification/product code context (when applicable)
International regulations & standards (grounded mapping):

EU MDR (2017/745) / IVDR (2017/746) where relevant
IMDRF guidance (e.g., clinical evaluation, SaMD)
ISO standards (e.g., ISO 10993, ISO 14971, ISO 13485, IEC 62304, IEC 60601 series) depending on device type
ASTM standards where appropriate (e.g., orthopedic mechanical testing)
4.2 Search Strategy (Design, Not Code)
The system must support two modes (selectable by deployment constraints):

Live Search Mode (preferred if allowed)
Uses a configurable web search connector or curated endpoint list (FDA pages, standards database pages).
Query generation must be derived from:
extracted device type / components / claims in the uploaded guidance
keywords and acronyms
identified risk areas (biocompatibility, sterilization, mechanical testing, software, cybersecurity, MRI, etc.)
2. Curated Offline Mode (fallback)

Uses a bundled or periodically refreshed curated dataset (e.g., a small index of FDA guidance titles + URLs + key excerpts; recognized standards snapshots).
This mode must still produce citations, but may be limited in coverage.
4.3 Grounding & Citation Requirements
The report must be citation-driven:

Every major requirement or recommendation must be supported by:
(a) the provided guidance text, or
(b) an external authoritative source, or
(c) clearly labeled expert synthesis (explicitly marked as interpretation)
Citation format (Markdown standard):

Inline numeric citations: ...text...[1][2]
A “References” section listing:
Title
Organization (FDA/ISO/IMDRF/TFDA/etc.)
URL
Access date
Notes on relevance
Traceability appendix (required):

A table mapping:
Input guidance section → extracted requirement → external corroborating source(s) → recommended evidence/artifacts
5. New Capability C: Two-Stage Report Generation Workflow
5.1 Stage 1 Agent: “Comprehensive Research Report” (2000–3000 words)
User controls (must exist):

Prompt editor (pre-filled with a robust default)
Model selector (Gemini only: gemini-2.5-flash, gemini-3-flash-preview)
Output language selector (TC/EN)
Max tokens & temperature controls (bounded defaults)
Agent responsibilities:

Summarize the uploaded guidance and extract:
scope, device type, intended use, key technical requirements, testing expectations, document checklist themes
Conduct FDA/international research as per §4
Produce a report in Markdown, 2000–3000 words, with:
Executive summary
Document synopsis (what the uploaded guidance is requiring)
FDA alignment analysis (potential pathways; 510(k) relevance; typical submission elements)
Standards landscape (recognized consensus standards + ISO/IEC/ASTM mapping)
International regulatory mapping (EU MDR/IMDRF highlights)
Risk & evidence expectations (biocompatibility/sterilization/mechanical/software, as applicable)
A practical checklist (derived, not copied blindly)
Traceability matrix + references
Post-processing UX:

Output shown in Markdown view with an optional “Text view”
User can edit directly
Download buttons: .md, .txt
5.2 Stage 2 Agent: “Template-Based Regulatory Report Rewriter”
Inputs:

Stage 1 report (editable, user-approved)
A template:
user-provided template (paste/upload)
or default templates library
Default template library (must include):

骨外固定器查驗登記審查指引與審查清單 (the provided guidance + checklist format)
Additional built-in templates (design requirement):
“FDA 510(k) Review Memo”
“Standards & Test Evidence Plan”
“Clinical/Nonclinical Evidence Summary”
Behavior:

Preserve the content fidelity but restructure into the template’s headings/tables
If the template contains a checklist table, populate it using the extracted requirements and research findings
Maintain references; ensure citations remain attached after restructuring
User controls:

Prompt/model selection (Gemini: gemini-2.5-flash, gemini-3-flash-preview)
Editable output + download .md/.txt
6. New Capability D: Skill Generator (skill.md) Creation Flow
6.1 Purpose
Enable users to automatically create a reusable agent skill definition (skill.md) that can generate new medical device guidance documents consistent with the structure and style found in the provided guidance.

6.2 Inputs
Original uploaded guidance (or its extracted structured outline)
Stage 2 template-based report
User-selected output language (TC/EN)
Optional user notes: “what to generalize,” “what must remain device-specific”
6.3 Output Requirements (skill-creator format)
The generated skill.md content must include:

YAML frontmatter:
name: stable, lowercase kebab-case
description: “pushy” trigger guidance (when to use)
optional compatibility (tools/dependencies)
A clear workflow section:
intent capture
input parsing
outline extraction
generation steps
quality checks
Output format template(s) for produced guidances
Example prompts (2–3)
Evaluation hints (qualitative checks)
6.4 Model Controls
Prompt editor and model selector:
gemini-2.5-flash
gemini-3-flash-preview
gemini-3.1-flash-lite-preview
Output editable; download as skill.md
6.5 “Ultrathink” Quality Constraints (Product Requirements)
The system must encourage “depth-first” generation:
Extract structure → identify requirement categories → generate reusable patterns → include checklists and traceability
Must avoid hallucinated citations in the skill content:
If including references, label them as “examples” unless sourced from the uploaded materials
7. API Key Handling (Enhanced, Must Match Requirements)
7.1 Environment-first, UI fallback
If an API key exists in the environment, the UI must:
indicate “loaded from environment”
not display the secret value
If not found, the UI must provide a secure password input on the webpage for:
OpenAI, Gemini, Anthropic, Grok
Keys entered in UI are:
stored only in Streamlit session state
never written to logs, downloads, or YAML exports
7.2 Key Visibility & Redaction
Any “Run History” or debugging panel must redact secrets.
If a user pastes a key into a document input, the system must warn and offer redaction assistance (see WOW feature in §9.2).
8. Agent & Pipeline Design (agents.yaml-driven)
8.1 New Agents (Conceptual Definitions)
Add new agent entries (configuration-only, no code changes implied) with parameters:

system_prompt (role, grounding rules, output language instructions)
default_model (Gemini for research/skill generator steps)
max_tokens defaults (higher for 2000–3000 words)
temperature defaults (lower for regulatory accuracy)
New agents:

guidance_research_agent – performs document analysis + external research plan + source retrieval summary
regulatory_report_agent – writes 2000–3000 word grounded report
template_report_agent – restructures into chosen template + checklist
skill_md_generator_agent – generates skill.md in skill-creator format
8.2 Agent Chaining UX (Preserve & Extend)
Each agent step runs “one-by-one”
Before executing each step:
user can edit prompt
user can select model
user can edit the previous step output (as the next step input)
Provide “Use Output as Next Input” convenience controls
Provide a “Diff vs Previous” viewer for iterative refinement (see WOW feature §9.1)
8.3 Three “WOW” Features Embedded Inside Generated skill.md
The skill generated by skill_md_generator_agent must include these 3 advanced features as explicit instructions:

Guidance Structure Fingerprinting + Auto-Outline Recovery
The skill instructs the model to derive a normalized outline from any similar guidance (even messy PDFs), recover missing headings, and maintain consistent numbering.
2. Requirement-to-Evidence Traceability Builder

The skill mandates generating a traceability matrix mapping each requirement to:
suggested evidence artifacts
applicable standards
verification method (test/inspection/analysis)
3. Bilingual Terminology Consistency Table (TC/EN)

Even when output is single-language, the skill produces a terminology table to ensure consistent translations of technical terms (device parts, tests, standards names), reducing regulatory ambiguity.
9. Three Additional WOW AI Features (Product-Level Additions)
These are new AI features added to the system (separate from Note Keeper Magics) and available as optional tools in the regulatory workspace.

9.1 WOW Feature #1: “Regulatory Diff & Version Timeline”
Every agent run can be snapshotted as a version.
Users can compare:
prompt changes
output diffs (Markdown-aware diff)
citation/reference changes
Includes a “what changed and why it matters” AI summary (user-controlled prompt/model).
9.2 WOW Feature #2: “Prompt Injection & Secret Leakage Shield”
When ingesting uploaded guidance or pasted content, run a safety scan that:
detects prompt-injection patterns (e.g., “ignore previous instructions”)
detects accidental secrets (API keys, tokens)
Produces a redaction suggestion report and a “sanitized copy” output users can adopt before running research agents.
9.3 WOW Feature #3: “Standards Crosswalk Matrix Generator”
From the report, automatically generate a matrix:
Requirement category → candidate standards (ISO/IEC/ASTM) → rationale → expected test evidence
Exports to Markdown and CSV.
Supports user keyword constraints (e.g., “focus on sterilization + biocompatibility only”).
10. Dashboard & Status Indicators (Enhanced)
10.1 Status Indicators
Maintain existing run statuses and expand to a “pipeline status bar” per workflow:

Ingestion: ready/processing/done
Research: queued/running/done/error
Report: queued/running/done/error
Template rewrite: queued/running/done/error
Skill creation: queued/running/done/error
10.2 Interactive Dashboard Additions
Add dashboard widgets (visual + functional):

“Active Workspace” card: current document, language, template selected
“Citation Coverage Meter”: % of paragraphs containing citations, plus warnings for unsupported claims
“Token/Cost Awareness” panel (estimates): per agent step token estimate and run count
11. Data Model & Artifact Management (Session + Downloads)
11.1 Core Artifacts
The system should treat each workflow output as a named artifact:

source_guidance_raw
source_guidance_extracted
research_sources_list
report_v1_comprehensive
report_v2_template
skill_md_v1
Artifacts must support:

editable text buffers
metadata: model, prompt hash, time, language, template ID
export to .md, .txt, and for some matrices .csv
11.2 References Store (Conceptual)
Maintain a reference list associated with a report:

each entry: title, org, url, access date, excerpt/snippet, relevance tags
used to regenerate references and traceability tables consistently
12. Quality, Compliance, and Safety Requirements
12.1 Non-Hallucination Guardrails
The report must clearly separate:
extracted content from user-provided guidance
external sourced statements (with citations)
interpretation (explicitly labeled)
12.2 Medical/Regulatory Disclaimer
Outputs must include a footer disclaimer:
informational use; not legal advice; verify with official sources
12.3 Reproducibility
Each generated report should include a “Generation Metadata” appendix:
date/time
model ID
language
template used
list of queries (if allowed) or at least query themes
13. Deployment on Hugging Face Spaces (Operational Requirements)
Streamlit app configured for HF Space environment
Environment secrets supported (HF “Secrets”)
Outbound network policy considered:
if live search is blocked, system switches to curated offline mode
Rate limiting and retries per provider
Observability:
run logs exclude secrets
capture errors with user-friendly remediation hints
14. Acceptance Criteria (High-Level)
Users can upload a PDF guidance and get a grounded 2000–3000 word Markdown report with references.
Users can switch output language TC/EN and see full localization of headings and narrative.
Users can apply the default Orthopedic External Fixators template and produce a matching checklist structure.
Users can generate skill.md in the selected language with the 3 embedded WOW features.
Users can override prompt and choose models for all LLM-related functions.
API keys: environment keys never shown; UI input appears only when missing.
20 Comprehensive Follow-Up Questions
For “FDA search,” do you want strictly FDA domains (fda.gov) or also include partner sources (e.g., accessdata.fda.gov, Federal Register, govinfo.gov, NIH/NLM) when relevant?
Should the system store a local cache of retrieved pages/excerpts for reproducibility, or only store URLs + snippets?
Do you require a strict citation rule such as “every paragraph must have at least one citation,” or only for normative requirements and recommendations?
When the uploaded guidance is not device-specific (e.g., general quality system guidance), should the report still infer a device category, or remain device-agnostic?
How should the system behave when it cannot find any relevant 510(k) summaries—omit the section, or include a “search performed but none found” statement?
For international mapping, which jurisdictions are highest priority beyond FDA/Taiwan: EU MDR, UKCA, Canada (Health Canada), Japan (PMDA), Australia (TGA), others?
Do you want the report to explicitly distinguish regulatory requirements vs recommended best practices vs common reviewer expectations?
Should the default template library be editable by users via the Agents Config Studio (stored in YAML/text), or kept as fixed built-ins?
In the Orthopedic External Fixators default checklist, do you want the system to preserve the exact table columns and checkbox style, or is a “structurally similar” checklist acceptable?
Do you want the system to generate an additional “submission-ready evidence index” (documents + filenames + responsible owner) as part of the template-based output?
For prompt injection shielding, should the system automatically sanitize content before running agents, or only suggest a sanitized copy and let the user choose?
Should users be able to run the research in two phases: (a) produce a research plan + queries, (b) confirm, then execute retrieval/synthesis?
What level of detail should standards mapping include—just standard numbers and titles, or also clause-level mappings (e.g., ISO 10993-1 endpoints and rationale)?
Should the system support device software/cybersecurity sections by default (IEC 62304, IEC 81001-5-1, FDA cybersecurity guidance), or only when the input guidance indicates software/network features?
How should the system handle paywalled standards (ISO/IEC full text)? Should it cite titles only and avoid implying access to the full document?
For the skill.md generation, do you want the skill to be generic across device types, or optimized to the uploaded guidance’s domain (e.g., orthopedic implants/fixators)?
Should the generated skill include built-in evaluation prompts and a scoring rubric (qualitative checklist) to help users test skill performance?
Do you want “Diff & Version Timeline” to persist across sessions (requiring storage) or be session-only (simpler, ephemeral)?
For file downloads, do you also need .docx export (in addition to .txt/.md), or must the system remain Markdown-first?
What are your preferred success metrics: time saved per review, citation completeness rate, checklist accuracy (human judged), or alignment with internal QA/regulatory standards?

Super please create a comprehensive technical specification based on previous design by keeping all original features and adding new features in markdown in 2000~3000 words that user can paste medical application summary (txt, markdown). The agent will use previous created skill.md to create a comprehensive review report in markdown in 2000~3000 words. User can modify the results, download or keep promping on the report. Ending with 20 comprehensive follow up questions.Agentic Medical Device Reviewer – Improved System Technical Specification (v2)
Target platform: Hugging Face Spaces (Streamlit) • Config-driven agents via agents.yaml • Multi-LLM (OpenAI, Gemini, Anthropic, Grok)

1. Purpose & Scope
This specification defines an improved design for the Agentic Medical Device Reviewer system. It preserves all original features (multi-tab Streamlit app, WOW UI themes/styles, agent pipeline execution with editable handoffs, TFDA premarket workflows, FDA 510(k) intelligence and review pipeline, PDF→Markdown conversion, Note Keeper with AI Magics, agents.yaml studio, dashboard/history) and adds new features for:

Published Guidance Ingestion + FDA/International Regulatory Research Report Generation
Users can paste or upload published guidance in TXT / Markdown / PDF.
Users select output language: Traditional Chinese (default) or English.
A research agent analyzes the provided document, searches and retrieves FDA-related information (e.g., 510(k) summaries, FDA guidance, FDA Recognized Consensus Standards), plus relevant international regulations and industry standards, then synthesizes everything into a grounded, citation-rich Markdown report (2000–3000 words).
Users can modify prompts and select models (restricted for this feature to Gemini: gemini-2.5-flash, gemini-3-flash-preview).
Users can edit results and download as .txt or .md.
2. Template-Based Report Rewriter

Users can provide a regulatory report template (paste/upload) or select a default template library (including the provided Orthopedic External Fixators guidance+checklist template).
A second agent rewrites the comprehensive report to match the chosen template, still grounded, with consistent section mapping.
Users can modify prompt/model (Gemini models above), edit outputs, and download.
3. Skill Generator (skill.md) for New Agent Skill Creation

From the final template-based report + the original guidance structure, a third agent generates a skill.md file content that defines a new agent skill in the standard skill-creator format.
Output language matches the user selection (TC/EN).
Users can modify prompt and select models (gemini-2.5-flash, gemini-3-flash-preview, gemini-3.1-flash-lite-preview).
Adds 3 “WOW” features inside the generated skill (defined in §8.3).
Additionally, the system adds 3 new “WOW AI features” across the product (beyond existing Note Keeper Magics), and upgrades the dashboard/status indicators, while maintaining the existing API key handling behavior with an enhancement: users can input keys on the webpage if environment keys are absent, and environment-provided keys are never displayed.

2. Baseline (Original) Capabilities – Must Remain Intact
2.1 UI & Experience
Streamlit multi-tab application with a “WOW UI” layer:
Light/Dark theme toggle
English / Traditional Chinese UI language
20 painter-inspired styles and a Jackpot random style picker
Global sidebar settings: default model, temperature, max tokens
Status indicators (pending/running/done/error) for agent runs
An interactive dashboard with run history and charts
2.2 LLM & Agent Orchestration
Multi-provider LLM routing:
OpenAI: gpt-4o-mini, gpt-4.1-mini
Gemini: gemini-2.5-flash, gemini-3-flash-preview, gemini-2.5-flash-lite, gemini-3.1-flash-lite-preview
Anthropic models (configurable)
Grok: grok-4-fast-reasoning, grok-3-mini
Agent definitions loaded from agents.yaml with a UI editor/studio
Sequential agent execution:
Users can edit prompt and choose model per agent
Users can edit outputs (text/markdown modes) and pass as input to the next agent
2.3 Regulatory Workflows
TFDA premarket tab:
Application import/export (JSON/CSV), completeness indicator
Guidance ingestion and pre-screening agents
Application markdown drafting and improvement
FDA 510(k) intelligence and review pipeline
PDF → Markdown conversion
Note Keeper:
Paste note → organized Markdown with highlighted keywords
User-editable note views
AI Magics (including AI Keywords with user-defined color)
2.4 Deployment & Ops
Deployed on Hugging Face Spaces using Streamlit
Uses environment variables for secrets when available; session state for runtime values
Works without code modifications through agents.yaml extensibility
3. New Capability A: Published Guidance Ingestion + Regulatory Research Report
3.1 User Goals
Upload/paste a published guidance (e.g., TFDA review guidance, internal SOP, public regulatory guidance).
Produce a credible, grounded report that:
Extracts key requirements from the input guidance
Identifies FDA-aligned pathways and evidence expectations
Cross-references FDA sources (510(k) summaries, guidance, recognized standards)
Extends to international regulations (EU MDR/IVDR as applicable, IMDRF, ISO/IEC standards, etc.)
Outputs in Traditional Chinese (default) or English
Includes citations and a research trail suitable for regulatory teams
3.2 Input Types & Ingestion Requirements
Supported inputs (single or multiple):

Paste: plain text / Markdown
Upload: .txt, .md, .pdf
Ingestion processing (design requirements):

PDF text extraction:
Page-by-page extraction with page boundary markers for traceability
Store extracted text plus metadata: filename, upload timestamp, page count, extraction warnings
Markdown/TXT normalization:
Preserve headings and lists if present
Detect encoding issues (e.g., mixed Chinese punctuation) and normalize
Document fingerprinting:
Compute a “structure signature” (e.g., heading outline + section keywords) used later for template mapping and skill creation
Language detection (non-blocking):
Detect primary language of input to guide bilingual term consistency, but output language is always user-selected
3.3 Output Language Control
Output language selector on the feature panel:
繁體中文 (default)
English
The selection must propagate to:
Prompts (system/user)
Report headings and table labels
Generated skill.md language
4. New Capability B: FDA + International Research (Search & Grounding)
4.1 Research Sources (Target Corpus)
The research agent must prioritize official and reputable sources:

FDA-related (required emphasis):

FDA Guidance documents (device-specific and general)
FDA Recognized Consensus Standards database
FDA 510(k) database:
510(k) summaries (when publicly available)
device classification/product code context (when applicable)
International regulations & standards (grounded mapping):

EU MDR (2017/745) / IVDR (2017/746) where relevant
IMDRF guidance (e.g., clinical evaluation, SaMD)
ISO standards (e.g., ISO 10993, ISO 14971, ISO 13485, IEC 62304, IEC 60601 series) depending on device type
ASTM standards where appropriate (e.g., orthopedic mechanical testing)
4.2 Search Strategy (Design, Not Code)
The system must support two modes (selectable by deployment constraints):

Live Search Mode (preferred if allowed)
Uses a configurable web search connector or curated endpoint list (FDA pages, standards database pages).
Query generation must be derived from:
extracted device type / components / claims in the uploaded guidance
keywords and acronyms
identified risk areas (biocompatibility, sterilization, mechanical testing, software, cybersecurity, MRI, etc.)
2. Curated Offline Mode (fallback)

Uses a bundled or periodically refreshed curated dataset (e.g., a small index of FDA guidance titles + URLs + key excerpts; recognized standards snapshots).
This mode must still produce citations, but may be limited in coverage.
4.3 Grounding & Citation Requirements
The report must be citation-driven:

Every major requirement or recommendation must be supported by:
(a) the provided guidance text, or
(b) an external authoritative source, or
(c) clearly labeled expert synthesis (explicitly marked as interpretation)
Citation format (Markdown standard):

Inline numeric citations: ...text...[1][2]
A “References” section listing:
Title
Organization (FDA/ISO/IMDRF/TFDA/etc.)
URL
Access date
Notes on relevance
Traceability appendix (required):

A table mapping:
Input guidance section → extracted requirement → external corroborating source(s) → recommended evidence/artifacts
5. New Capability C: Two-Stage Report Generation Workflow
5.1 Stage 1 Agent: “Comprehensive Research Report” (2000–3000 words)
User controls (must exist):

Prompt editor (pre-filled with a robust default)
Model selector (Gemini only: gemini-2.5-flash, gemini-3-flash-preview)
Output language selector (TC/EN)
Max tokens & temperature controls (bounded defaults)
Agent responsibilities:

Summarize the uploaded guidance and extract:
scope, device type, intended use, key technical requirements, testing expectations, document checklist themes
Conduct FDA/international research as per §4
Produce a report in Markdown, 2000–3000 words, with:
Executive summary
Document synopsis (what the uploaded guidance is requiring)
FDA alignment analysis (potential pathways; 510(k) relevance; typical submission elements)
Standards landscape (recognized consensus standards + ISO/IEC/ASTM mapping)
International regulatory mapping (EU MDR/IMDRF highlights)
Risk & evidence expectations (biocompatibility/sterilization/mechanical/software, as applicable)
A practical checklist (derived, not copied blindly)
Traceability matrix + references
Post-processing UX:

Output shown in Markdown view with an optional “Text view”
User can edit directly
Download buttons: .md, .txt
5.2 Stage 2 Agent: “Template-Based Regulatory Report Rewriter”
Inputs:

Stage 1 report (editable, user-approved)
A template:
user-provided template (paste/upload)
or default templates library
Default template library (must include):

骨外固定器查驗登記審查指引與審查清單 (the provided guidance + checklist format)
Additional built-in templates (design requirement):
“FDA 510(k) Review Memo”
“Standards & Test Evidence Plan”
“Clinical/Nonclinical Evidence Summary”
Behavior:

Preserve the content fidelity but restructure into the template’s headings/tables
If the template contains a checklist table, populate it using the extracted requirements and research findings
Maintain references; ensure citations remain attached after restructuring
User controls:

Prompt/model selection (Gemini: gemini-2.5-flash, gemini-3-flash-preview)
Editable output + download .md/.txt
6. New Capability D: Skill Generator (skill.md) Creation Flow
6.1 Purpose
Enable users to automatically create a reusable agent skill definition (skill.md) that can generate new medical device guidance documents consistent with the structure and style found in the provided guidance.

6.2 Inputs
Original uploaded guidance (or its extracted structured outline)
Stage 2 template-based report
User-selected output language (TC/EN)
Optional user notes: “what to generalize,” “what must remain device-specific”
6.3 Output Requirements (skill-creator format)
The generated skill.md content must include:

YAML frontmatter:
name: stable, lowercase kebab-case
description: “pushy” trigger guidance (when to use)
optional compatibility (tools/dependencies)
A clear workflow section:
intent capture
input parsing
outline extraction
generation steps
quality checks
Output format template(s) for produced guidances
Example prompts (2–3)
Evaluation hints (qualitative checks)
6.4 Model Controls
Prompt editor and model selector:
gemini-2.5-flash
gemini-3-flash-preview
gemini-3.1-flash-lite-preview
Output editable; download as skill.md
6.5 “Ultrathink” Quality Constraints (Product Requirements)
The system must encourage “depth-first” generation:
Extract structure → identify requirement categories → generate reusable patterns → include checklists and traceability
Must avoid hallucinated citations in the skill content:
If including references, label them as “examples” unless sourced from the uploaded materials
7. API Key Handling (Enhanced, Must Match Requirements)
7.1 Environment-first, UI fallback
If an API key exists in the environment, the UI must:
indicate “loaded from environment”
not display the secret value
If not found, the UI must provide a secure password input on the webpage for:
OpenAI, Gemini, Anthropic, Grok
Keys entered in UI are:
stored only in Streamlit session state
never written to logs, downloads, or YAML exports
7.2 Key Visibility & Redaction
Any “Run History” or debugging panel must redact secrets.
If a user pastes a key into a document input, the system must warn and offer redaction assistance (see WOW feature in §9.2).
8. Agent & Pipeline Design (agents.yaml-driven)
8.1 New Agents (Conceptual Definitions)
Add new agent entries (configuration-only, no code changes implied) with parameters:

system_prompt (role, grounding rules, output language instructions)
default_model (Gemini for research/skill generator steps)
max_tokens defaults (higher for 2000–3000 words)
temperature defaults (lower for regulatory accuracy)
New agents:

guidance_research_agent – performs document analysis + external research plan + source retrieval summary
regulatory_report_agent – writes 2000–3000 word grounded report
template_report_agent – restructures into chosen template + checklist
skill_md_generator_agent – generates skill.md in skill-creator format
8.2 Agent Chaining UX (Preserve & Extend)
Each agent step runs “one-by-one”
Before executing each step:
user can edit prompt
user can select model
user can edit the previous step output (as the next step input)
Provide “Use Output as Next Input” convenience controls
Provide a “Diff vs Previous” viewer for iterative refinement (see WOW feature §9.1)
8.3 Three “WOW” Features Embedded Inside Generated skill.md
The skill generated by skill_md_generator_agent must include these 3 advanced features as explicit instructions:

Guidance Structure Fingerprinting + Auto-Outline Recovery
The skill instructs the model to derive a normalized outline from any similar guidance (even messy PDFs), recover missing headings, and maintain consistent numbering.
2. Requirement-to-Evidence Traceability Builder

The skill mandates generating a traceability matrix mapping each requirement to:
suggested evidence artifacts
applicable standards
verification method (test/inspection/analysis)
3. Bilingual Terminology Consistency Table (TC/EN)

Even when output is single-language, the skill produces a terminology table to ensure consistent translations of technical terms (device parts, tests, standards names), reducing regulatory ambiguity.
9. Three Additional WOW AI Features (Product-Level Additions)
These are new AI features added to the system (separate from Note Keeper Magics) and available as optional tools in the regulatory workspace.

9.1 WOW Feature #1: “Regulatory Diff & Version Timeline”
Every agent run can be snapshotted as a version.
Users can compare:
prompt changes
output diffs (Markdown-aware diff)
citation/reference changes
Includes a “what changed and why it matters” AI summary (user-controlled prompt/model).
9.2 WOW Feature #2: “Prompt Injection & Secret Leakage Shield”
When ingesting uploaded guidance or pasted content, run a safety scan that:
detects prompt-injection patterns (e.g., “ignore previous instructions”)
detects accidental secrets (API keys, tokens)
Produces a redaction suggestion report and a “sanitized copy” output users can adopt before running research agents.
9.3 WOW Feature #3: “Standards Crosswalk Matrix Generator”
From the report, automatically generate a matrix:
Requirement category → candidate standards (ISO/IEC/ASTM) → rationale → expected test evidence
Exports to Markdown and CSV.
Supports user keyword constraints (e.g., “focus on sterilization + biocompatibility only”).
10. Dashboard & Status Indicators (Enhanced)
10.1 Status Indicators
Maintain existing run statuses and expand to a “pipeline status bar” per workflow:

Ingestion: ready/processing/done
Research: queued/running/done/error
Report: queued/running/done/error
Template rewrite: queued/running/done/error
Skill creation: queued/running/done/error
10.2 Interactive Dashboard Additions
Add dashboard widgets (visual + functional):

“Active Workspace” card: current document, language, template selected
“Citation Coverage Meter”: % of paragraphs containing citations, plus warnings for unsupported claims
“Token/Cost Awareness” panel (estimates): per agent step token estimate and run count
11. Data Model & Artifact Management (Session + Downloads)
11.1 Core Artifacts
The system should treat each workflow output as a named artifact:

source_guidance_raw
source_guidance_extracted
research_sources_list
report_v1_comprehensive
report_v2_template
skill_md_v1
Artifacts must support:

editable text buffers
metadata: model, prompt hash, time, language, template ID
export to .md, .txt, and for some matrices .csv
11.2 References Store (Conceptual)
Maintain a reference list associated with a report:

each entry: title, org, url, access date, excerpt/snippet, relevance tags
used to regenerate references and traceability tables consistently
12. Quality, Compliance, and Safety Requirements
12.1 Non-Hallucination Guardrails
The report must clearly separate:
extracted content from user-provided guidance
external sourced statements (with citations)
interpretation (explicitly labeled)
12.2 Medical/Regulatory Disclaimer
Outputs must include a footer disclaimer:
informational use; not legal advice; verify with official sources
12.3 Reproducibility
Each generated report should include a “Generation Metadata” appendix:
date/time
model ID
language
template used
list of queries (if allowed) or at least query themes
13. Deployment on Hugging Face Spaces (Operational Requirements)
Streamlit app configured for HF Space environment
Environment secrets supported (HF “Secrets”)
Outbound network policy considered:
if live search is blocked, system switches to curated offline mode
Rate limiting and retries per provider
Observability:
run logs exclude secrets
capture errors with user-friendly remediation hints
14. Acceptance Criteria (High-Level)
Users can upload a PDF guidance and get a grounded 2000–3000 word Markdown report with references.
Users can switch output language TC/EN and see full localization of headings and narrative.
Users can apply the default Orthopedic External Fixators template and produce a matching checklist structure.
Users can generate skill.md in the selected language with the 3 embedded WOW features.
Users can override prompt and choose models for all LLM-related functions.
API keys: environment keys never shown; UI input appears only when missing.
20 Comprehensive Follow-Up Questions
For “FDA search,” do you want strictly FDA domains (fda.gov) or also include partner sources (e.g., accessdata.fda.gov, Federal Register, govinfo.gov, NIH/NLM) when relevant?
Should the system store a local cache of retrieved pages/excerpts for reproducibility, or only store URLs + snippets?
Do you require a strict citation rule such as “every paragraph must have at least one citation,” or only for normative requirements and recommendations?
When the uploaded guidance is not device-specific (e.g., general quality system guidance), should the report still infer a device category, or remain device-agnostic?
How should the system behave when it cannot find any relevant 510(k) summaries—omit the section, or include a “search performed but none found” statement?
For international mapping, which jurisdictions are highest priority beyond FDA/Taiwan: EU MDR, UKCA, Canada (Health Canada), Japan (PMDA), Australia (TGA), others?
Do you want the report to explicitly distinguish regulatory requirements vs recommended best practices vs common reviewer expectations?
Should the default template library be editable by users via the Agents Config Studio (stored in YAML/text), or kept as fixed built-ins?
In the Orthopedic External Fixators default checklist, do you want the system to preserve the exact table columns and checkbox style, or is a “structurally similar” checklist acceptable?
Do you want the system to generate an additional “submission-ready evidence index” (documents + filenames + responsible owner) as part of the template-based output?
For prompt injection shielding, should the system automatically sanitize content before running agents, or only suggest a sanitized copy and let the user choose?
Should users be able to run the research in two phases: (a) produce a research plan + queries, (b) confirm, then execute retrieval/synthesis?
What level of detail should standards mapping include—just standard numbers and titles, or also clause-level mappings (e.g., ISO 10993-1 endpoints and rationale)?
Should the system support device software/cybersecurity sections by default (IEC 62304, IEC 81001-5-1, FDA cybersecurity guidance), or only when the input guidance indicates software/network features?
How should the system handle paywalled standards (ISO/IEC full text)? Should it cite titles only and avoid implying access to the full document?
For the skill.md generation, do you want the skill to be generic across device types, or optimized to the uploaded guidance’s domain (e.g., orthopedic implants/fixators)?
Should the generated skill include built-in evaluation prompts and a scoring rubric (qualitative checklist) to help users test skill performance?
Do you want “Diff & Version Timeline” to persist across sessions (requiring storage) or be session-only (simpler, ephemeral)?
For file downloads, do you also need .docx export (in addition to .txt/.md), or must the system remain Markdown-first?
What are your preferred success metrics: time saved per review, citation completeness rate, checklist accuracy (human judged), or alignment with internal QA/regulatory standards?





----------転送メッセージ----------
From: Hannah Lin <joylovehannah@gmail.com>
日付: 2026年4月6日月曜日
件名: User-OPAL-040626
To: joylovesophia@gmail.com, joylovefreesia6@gmail.com, joylovecopilot@gmail.com, joylovejasmin@gmail.com, joylovepandora@gmail.com, joylovejexer@gmail.com, "joyalovejane@gmail.com" <joyalovejane@gmail.com>, "joyalovejennie@gmail.com" <joyalovejennie@gmail.com>


https://hannah-md-reg-040626-hmgnv4ad5i3s4amtywqu4f.streamlit.app/

https://github.com/Hannah012926/GEMINI3-WOW-MD-Reg-Hannah-040626

https://opal.google/edit/1c_uwO3yzrO4vGPk--i_nrSpnqhbCoRy7

https://aistudio.google.com/apps/fb62fb1c-f3ce-4921-bc58-0f689446b93e?showPreview=true&showAssistant=true

https://aistudio.google.com/apps/944bcc89-e898-4f96-879c-adff90a28629?showAssistant=true&showPreview=true

https://opal.google/edit/1Y3gzRj8v5jzTy4-ojpBiwRjlOfUVNUCh

https://opal.google/edit/1WAQo9QKhKwBtFiU3VVKjoMABkJvToXw7

https://jane-skill-040626-njkfownru9cpkxtq2tmkhn.streamlit.app/


https://github.com/Hamilton082325/Jane-SKill-040626/blob/main/app.py


Super, please create complete code (full features) of app.py. Please check and fix potential bugs before give results. Ending with 20 comprehensive follow up question.

Please let user to select light(default)/dark themes, traditional chinese(default)/english, 10 styles based on pantone color palette within the webpage


Super, please don't modify code and only create a comprehensive technical specification of this design in markdown in 3000~4000 words. Ending with 20 comprehensive follow up questions.


SmartMed Review 4.1 — Comprehensive Technical Specification (Streamlit on Hugging Face Spaces)
Document Version: 4.1.0
Date: 2026-03-19
Status: Draft Technical Specification (Design + Implementation Guidance; no code included)
System Name: SmartMed Review 4.1 (智慧醫材審查指引與清單生成系統)
Deployment Target: Hugging Face Spaces (Streamlit)
Key Addition vs 4.0: Step 3 “Guidance Markdown Generator” expanded to support OpenAI models (e.g., gpt-4o-mini) in addition to Gemini models, with robust key handling and reliability safeguards.

1. Executive Summary
SmartMed Review 4.1 is an AI-powered, agentic regulatory workspace designed for medical device regulatory affairs (RA) and reviewer workflows. It preserves all capabilities of SmartMed Review 3.0 and 4.0—document ingestion, OCR, guidance transformation into structured Markdown, submission triage, review memo/report drafting, note keeping with AI “Magics,” agent-by-agent orchestration from agents.yaml, multi-provider LLM routing (Gemini/OpenAI/Anthropic/Grok), and the WOW UI system—while adding a targeted but high-impact upgrade:

Step 3 — Generate Organized Guidance Markdown (2000–3000 words, exactly 3 tables) now supports OpenAI models (specifically gpt-4o-mini as requested) alongside existing Gemini models.

This Step 3 upgrade is implemented purely as a design-level change to the “model allowlist” and execution preflight logic for Step 3. The existing multi-provider routing and API-key handling infrastructure is reused.

1.1 Why Step 3 OpenAI Support Matters
Reliability/consistency: Some users may prefer OpenAI’s formatting behaviors for strict table count and structured Markdown.
Operational flexibility: Enterprises frequently standardize on a provider; adding OpenAI to Step 3 enables consistent governance across modules.
Failover and redundancy (future-ready): Supporting multiple providers for the same high-value workflow enables safer production operations.
1.2 Primary Users
Regulatory Affairs specialists preparing and interpreting premarket submission review guidance.
Medical device reviewers drafting review memos and identifying gaps.
Quality / compliance professionals ensuring submission completeness and traceability.
Technical leads maintaining agents.yaml and deploying on Spaces.
2. System Scope and Design Principles
2.1 In-Scope Modules (Retained + Enhanced)
Dashboard (WOW status + metrics)
Guidance OCR & Generator
Paste or upload TXT/MD/PDF
PDF preview + page selection
OCR via Python packages (best-effort) or LLM-based OCR via Gemini Vision
Step 3 Markdown guidance generation (2000–3000 words, exactly 3 tables)
NEW: Step 3 model selector includes OpenAI gpt-4o-mini
510(k) Intelligence
PDF → Markdown transformer
Summary & Entities
Comparator (old vs new PDF comparisons)
Checklist & Report
AI Note Keeper & Magics
FDA Orchestration
Dynamic Agents from Guidance
SKILL Panel (SKILL.md rendering)
2.2 Non-Goals
No persistent multi-user accounts, RBAC, audit DB, or long-term storage mandated.
No claim of legal/regulatory authority; outputs are drafting aids.
No fully deterministic compliance enforcement guaranteed—LLM outputs are probabilistic.
2.3 Core Principles
Human-in-the-loop control: Users can select pages, choose OCR methods/models, edit prompts, and edit outputs at each stage.
Environment-first security: API keys are obtained from environment secrets first; UI key entry is fallback only.
Provider-agnostic orchestration: All core generation operations use the same unified LLM call interface and model-routing logic.
WOW UX without sacrificing clarity: High visual polish, but with transparent status indicators, diagnostics, and error messages.
Graceful degradation: If optional dependencies (PyMuPDF, Pillow, pytesseract) are missing, core text ingestion still works.
3. High-Level Architecture (Streamlit + agents.yaml + Multi-LLM Routing)
3.1 Runtime Components
A. Streamlit UI Layer

Sidebar: global settings (theme, language, Pantone palette, painter style, default model/max_tokens/temperature), API key handling, and optional agents.yaml upload override.
Main tabs: module views and workflows.
B. Session State Layer

Stores runtime-only artifacts:
Uploaded PDF bytes (ephemeral)
OCR-selected pages
Extracted raw text (per page + merged)
Generated Markdown guidance
Prompts (pinned)
Agent outputs (editable)
Run history events (for dashboard)
No disk persistence required beyond ephemeral caching.
C. Document Processing Layer

PDF text extraction via pypdf
Optional PDF render → images via PyMuPDF/Pillow
Optional python OCR via pytesseract (if system Tesseract is installed)
Gemini Vision OCR for scanned pages (LLM OCR option)
D. LLM Integration Layer

One unified call entry point, routing by model to:
OpenAI (Chat Completions)
Gemini (generate_content)
Anthropic (messages)
Grok (xAI REST)
E. Agent Orchestration Layer (agents.yaml)

Defines agents (system prompt, templates, defaults).
Agent UI allows prompt/model/max_tokens override before execution.
Editable output is carried forward as input to next agent.
3.2 Step 3 Upgrade: OpenAI Model Support
The Step 3 “Guidance Generator” module previously restricted model selection to:

gemini-2.5-flash
gemini-3-flash-preview
In 4.1, Step 3 expands allowlist to include:

gpt-4o-mini (OpenAI)
This is a targeted change to:

Step 3 model selection UI list (allow OpenAI model)
Step 3 execution preflight checks (ensure OpenAI key availability)
No change to global routing logic is required because OpenAI is already supported system-wide.
4. WOW UI Specification (Theme, Language, Painter Styles, Pantone Palettes)
4.1 Global UI Controls (Sidebar)
Theme: Light / Dark
Language: English / Traditional Chinese (繁體中文)
Pantone Palette Style (10): influences primary colors, accents, surface backgrounds, warnings/errors/success, and the coral highlight tone.
Painter Style (20): background gradients and aesthetic personality layers.
Jackpot: random painter style selection.
Default Model / Default max_tokens / Temperature: used across modules as the default, but each step can override.
4.2 Status Indicators (WOW)
Running/pending/done/error dots with animated pulse while running.
Module-level statuses:
Guidance Workspace (ingestion/OCR)
Guidance Generator (Step 3)
Skill Apply
Each agent run status (agent-by-agent pipeline)
4.3 Dashboard (Observability UX)
Total runs, 510(k) runs, approximate token usage.
Charts:
Runs by tab
Runs by model
Approx tokens over time
Recent activity data table
5. API Key Management (Environment-First, UI Fallback)
5.1 Requirements
If an environment key exists (e.g., OPENAI_API_KEY), the UI must only show “managed by environment” and must not display the key.
If missing, show a password input field for user entry.
Session-stored keys must remain in memory only, not logged or written to disk.
5.2 Step 3 Specific Requirement: OpenAI Preflight
Because Step 3 now offers OpenAI models, it must:

Determine provider based on chosen model.
If provider is OpenAI and no OpenAI key is available:
Block execution early with a clear warning (not a cryptic exception).
Keep status consistent: do not flip to running if execution is blocked.
This avoids common UX and reliability issues (e.g., “Generate” → immediate error).

6. Guidance OCR & Generator Module (Medical Guidance Ingestion + OCR + Step 3 Generation)
This module is a centerpiece of SmartMed Review 4.x and now includes a provider-flexible Step 3.

6.1 Step 1 — Ingest Guidance (Paste or Upload)
Supported inputs:

Paste text/markdown
Upload:
.txt, .md (decode as UTF-8 with error ignoring)
.pdf (store bytes in session state)
Operational behavior:

If both paste and file exist, file content takes precedence unless user indicates otherwise (recommended: explicit “Use paste” or “Use file” selection—optional enhancement).
6.2 Step 1b — PDF Preview and Page Selection
If PDF is uploaded:

Inline preview via embedded PDF viewer (iframe).
Detect page count.
Multi-select pages (1-based page indices).
Default selection should be small (first few pages) to reduce accidental large OCR runs.
6.3 Step 2 — Extraction / OCR
Two extraction modes:

A. Python Packages Mode (best-effort)
Use pypdf to extract text from selected pages.
Provide diagnostics per page (chars extracted, exceptions).
If extracted chars are very low, optionally attempt python OCR fallback (only if dependencies exist):
Render page images via PyMuPDF
OCR via pytesseract
This mode is economical but depends on PDF content quality and installed dependencies.

B. LLM-based OCR Mode (Gemini Vision)
Render selected PDF pages to images (requires PyMuPDF + Pillow).
Send each page image to Gemini Vision OCR prompt.
Models allowed:
gemini-2.5-flash
gemini-3-flash-preview
OCR prompt requirements:

Faithful transcription
Preserve headings and bullets
Reconstruct tables as Markdown tables when possible
Avoid hallucination
Avoid duplicating headers/footers
Performance safety requirements:

Page-limit guardrails (e.g., 40 pages per run) to prevent runaway costs and timeouts.
6.4 Step 2 Output: Normalized Raw Guidance Text
Regardless of extraction path, the system produces:

A merged “raw guidance text” artifact with page delimiters (e.g., [PDF Page 7]).
An “OCR diagnostics” artifact for transparency.
6.5 Step 3 — Generate Organized Guidance Markdown (2000–3000 words, exactly 3 tables)
This step transforms raw guidance text into a structured Markdown guidance document suitable for reviewer workflows.

6.5.1 Step 3 Inputs
Raw guidance text (from Step 2)
Output language toggle: English or Traditional Chinese
Editable user prompt (guidance generation prompt)
Model selection (now includes OpenAI)
max_tokens (default 12000, user-editable)
6.5.2 Step 3 Model Allowlist (4.1)
Allowed models for Step 3:

OpenAI: gpt-4o-mini (newly supported)
Gemini: gemini-2.5-flash, gemini-3-flash-preview
Design rationale:

These models are optimized for speed/cost relative to larger models while still supporting structured generation.
Step 3 outputs are long; user controls max_tokens to manage output length.
6.5.3 Step 3 Prompt Contract (Hard Constraints)
The system prompt and user prompt must enforce:

Language constraint

English OR Traditional Chinese
Length constraint

Strictly 2000–3000 words
(Note: in CJK, “word count” is heuristic; the UI must label it as such.)
Table constraint

Exactly 3 Markdown tables in the entire document.
No extra mini tables, no additional pipe-based formatting that resembles a table.
No hallucination constraint

Do not invent requirements not present in the guidance.
If guidance lacks details, state uncertainty and suggest what to confirm.
Structure expectations

Reviewer-friendly headings (scope, key review points, common deficiencies, evidence expectations).
3 tables should be meaningful (e.g., checklist, deficiencies/risks, mapping/standards).
6.5.4 Step 3 Execution Preflight (Key Addition)
When user clicks “Generate”:

Determine provider from selected model.
If provider is OpenAI:
Ensure OpenAI key is available via environment or session.
If missing, block and show a warning.
If provider is Gemini:
Ensure Gemini key is available, else block similarly.
This avoids status thrash (running → error) and makes the system predictable.

6.5.5 Step 3 Outputs
guidance_doc_md: generated Markdown document
guidance_doc_prompt_pinned: the final prompt used for generation (pinned for reproducibility)
Dashboard history event with:
model name
approximate token estimate
compliance metadata (word count estimate, table count estimate)
6.6 Step 4 — Edit & Download Guidance
Users can:

View/edit in Markdown or plain text.
Download:
.md
.txt
6.7 Step 5 — Keep Prompt / Apply Skill to Guidance Doc
Pinned prompt is displayed read-only for transparency.
Users can apply a described skill (one-off transformation) using any supported model, producing an editable output.
7. LLM Provider Routing and Compatibility Requirements
7.1 Routing Logic
Model → provider mapping:

gpt-* → OpenAI
gemini-* → Gemini
claude-* → Anthropic
grok-* → xAI Grok
Step 3 must use this same routing mechanism without special-casing. Adding gpt-4o-mini to Step 3 is therefore primarily an allowlist/UI matter plus key preflight.

7.2 Provider Differences That Impact Step 3
Output formatting behavior: OpenAI and Gemini may differ in how they create Markdown tables and adhere to “exactly N tables.”
Token accounting differences: max_tokens controls output tokens, but total context (input + output) must fit model context.
Error modes: 401/429 differences; Step 3 must surface clear errors and recommended mitigations (reduce pages, switch model, retry).
8. Validation and Quality Assurance for Step 3 Constraints
8.1 Compliance Checks (Heuristic)
After Step 3 generation, the UI runs checks:

Word count estimate (primarily for English; heuristic for Chinese)
Markdown table count estimate (heuristic via regex detecting header separators)
Results are displayed as a “Compliance Check” panel:

Word count estimate
Tables estimate
“Constraint OK?” indicator
8.2 Recommended Reliability Enhancements (Design-Level)
Even without code changes in this spec, the design supports:

“Regenerate with constraints” action when compliance fails (prompt remains editable).
Suggested user actions if output fails:
strengthen the prompt constraints
reduce input size (fewer pages)
try an alternate model (Gemini ↔ OpenAI)
8.3 Preventing False Positives in Table Counting
Because Markdown table detection is heuristic:

The prompt should discourage use of ASCII art that resembles tables.
The generator should avoid including extra tables in appendices.
9. Agent-Oriented Workflows (agents.yaml) and Output Chaining
9.1 Agent Execution Control
Before executing each agent:

User can modify prompt
User can set max_tokens (default 12000)
User can select models across providers
After execution:

Output is editable in Markdown or plain text
The edited output becomes input to the next agent (chain)
9.2 Integration with Guidance Doc
The Step 3 guidance output is designed to be:

directly editable and downloadable
optionally passed into downstream agents:
checklist conversion
memo drafting
risk analysis
standards mapping
The design intentionally keeps Step 3 output in a canonical “guidance_doc_effective” artifact so it can be reused across modules.

10. AI Note Keeper & Magics (Retained)
The Note Keeper transforms raw notes into organized Markdown and provides six “AI Magics” for secondary transformations. Keyword highlighting defaults to coral (tied to palette) and can be customized by the user in the AI Keywords magic. This module remains provider-flexible and supports prompt/model customization.

11. Security, Privacy, and Compliance Considerations
11.1 Data Handling
Content (PDF bytes, OCR text, guidance doc) is stored only in session state by default.
Downloads are user-initiated; no server-side persistence is required.
11.2 Key Handling
Never display environment keys.
UI keys stored in session state only.
Do not log keys in telemetry.
11.3 Regulatory Safety Disclaimers
The UI should display a persistent disclaimer:
“AI output is a draft. Regulatory decisions must be made by qualified professionals.”
For OCR and guidance generation:
If confidence is low (e.g., garbled OCR), prompt user to verify.
12. Deployment and Dependency Profile (Hugging Face Spaces)
12.1 Baseline Dependencies
Streamlit, pandas, altair, PyYAML, pypdf
OpenAI SDK, google-generativeai, anthropic, httpx
12.2 Optional Dependencies for OCR
PyMuPDF + Pillow (for PDF rendering to images)
pytesseract (requires system Tesseract binary; may need Spaces OS package installation support)
12.3 Graceful Degradation Rules
If optional libs are missing:

LLM OCR mode should warn and block (or hide) if required libs are absent.
Python OCR fallback should be “best-effort,” not assumed.
13. Observability and Operational Robustness
13.1 Event Logging
Each major action logs an event:

tab/module
agent/step name
model used
approximate token estimate
timestamps and optional compliance metadata
13.2 User-Facing Diagnostics
OCR diagnostics per page
Extraction warnings (e.g., caps on pages processed)
Model/provider key status
13.3 Common Failure Modes and Mitigations (Step 3 Focus)
Missing key → preflight warning (block run)
Rate limits → advise retry/backoff, switch model/provider, reduce input
Truncation → reduce input size, adjust max_tokens, or split the task
14. Acceptance Criteria (4.1, Step 3 OpenAI Upgrade)
Step 3 model selector includes gpt-4o-mini alongside Gemini models.
When gpt-4o-mini is selected and OpenAI key is missing, Step 3 blocks execution with a clear warning (no ambiguous crash).
When gpt-4o-mini is selected and key is present, Step 3 successfully generates a Markdown document.
Compliance check is applied uniformly regardless of provider, showing word count estimate and table count estimate.
Step 3 output remains editable and downloadable (.md, .txt), and the pinned prompt is preserved.
All original features remain functional and unchanged: OCR workflows, agent orchestration, note keeper, report generation, dashboard, theming, bilingual UI.
15. Comprehensive Follow-Up Questions (20)
Should Step 3’s OpenAI model list include only gpt-4o-mini, or also gpt-4.1-mini for improved constraint adherence and fewer regeneration cycles?
When OpenAI keys are missing, do you prefer hiding OpenAI models entirely in Step 3, or showing them but blocking execution with a preflight warning?
Do you want provider-specific default settings for Step 3 (e.g., temperature 0.1 for OpenAI, 0.2 for Gemini) to increase determinism?
Should Step 3 support output streaming (especially helpful for long 2000–3000 word documents), or remain non-streaming for simplicity?
Do you want Step 3 to implement a “repair pass” flow when constraints fail (e.g., wrong table count), instead of requiring manual prompt edits and regeneration?
For Traditional Chinese output, should the length constraint be measured by character count rather than word count, and what range would you prefer?
Should the compliance checker for “exactly 3 tables” be upgraded to a stricter Markdown parser to eliminate regex false positives/negatives?
Do you want the three tables to be fixed by design (Checklist / Common Deficiencies / Mapping), or dynamically chosen based on the guidance content?
Should Step 3 optionally include page citations using the [PDF Page X] markers to improve traceability and reviewer trust?
Should the UI warn users when the raw guidance input is above a threshold (e.g., character count/pages) indicating high risk of truncation or high cost?
Do you want a built-in “summarize/condense guidance” pre-step to reduce input size before Step 3 generation?
Should Step 3 allow a “strict template mode” that enforces a fixed heading structure to increase comparability across runs?
Should the system display a per-run cost estimate by model/provider in the dashboard (even if approximate), and what price table should be used?
Do you require an enterprise policy option to prevent sending content to certain providers (e.g., disable OpenAI in regulated environments) even if keys exist?
Should Step 3 store multiple output versions (history) to allow side-by-side comparison between Gemini and OpenAI results?
Should the pinned prompt include additional metadata (selected pages, OCR mode, OCR model) for reproducibility and audit readiness?
How should the system handle OpenAI/Gemini rate limiting in Step 3: manual retry only, or guided retry with exponential backoff and clear wait messaging?
Should Step 3 enforce minimum quality thresholds for each table (e.g., minimum rows/columns) to prevent “tiny dummy tables” satisfying the constraint?
Do you want Step 3 to be exposed as an agents.yaml agent as well (so it can be invoked inside the general agent pipeline), or remain a dedicated UI-only step?

Should Step 3 include an optional “regulatory terminology glossary lock” to keep bilingual translations consistent across runs and across providers?




Hi please improve previous design by keeping all original features and adding new features that user can paste or upload published guidance (txt, markdown, pdf). Then user select language for output (Traditional chinese(default)/Englilsh). Then agent analyze the user input information and  search to get FDA related information (510(k) summary, guidance, standard). Then agent create a comprehensive report in markdown in 2000~3000 words grounding to identify and research related international regulations, industry standards, and official guidance documents. Synthesize the analysis of the provided document with the external research findings to create a comprehensive report (user can modify prompt and select models, gemini-2.5-flash, gemini-3-flash-preview). User can modify results or download results(txt, markdown). Then User can provide a regultion report template or select default report template.  Then agent will create a comprehensive report based on previous comprehensive report using the report template(user can modify prompt and select models, gemini-2.5-flash, gemini-3-flash-preview). User can modify results or download results(txt, markdown). Then agent will create a  markdown content for a skill.md file that defines a new agent skill. This skill should be designed to generate comprehensive medical device guidance based on the structure and information found in the provided medical device guidance input. Use the standard skill-creator format for the description. The entire content must be written in the specified output language.  Please do ultrathink to get excellent results and add 3 additional wow features in this skill. Please use skill creator skill to create this skill.md (user can modify prompt and select models, gemini-2.5-flash, gemini-3-flash-preview). User can modify results or download results(skill.md).  Please let user to modify prompt and select models for llm related features. Please add 3 additional wow ai features (create by you). Please let user to select light/dark themes, english/traditional chinese, 20 styles based on famous painters. Sample publish guidance as attached. Please find sample results of review guidance with checklist:Default report template:骨外固定器查驗登記審查指引與審查清單 本文件旨在規範骨外固定器（Orthopedic External Fixators）於醫療器材查驗登記時之臨床前安全與有效性要求，確保產品符合應有之品質標準。
第一部分：骨外固定器臨床前審查指引 (Review Guidance)
1. 產品規格要求 (Product Specifications) 申請者應提供詳盡之產品資料，以評估其設計之合理性與安全性：
用途說明：詳列臨床適應症、適用對象及預定用途。 組件清單：應包含所有系統組件（如：骨針、連接桿、接合器、夾具等）。 工程圖面：檢附具備關鍵幾何尺寸、公差之主要組件工程圖。 材質證明：所有與人體接觸或具結構功能之材質，應標明符合之國際材質標準（如 ASTM F136, ISO 5832 等）。 等同性比較：與已上市類似品執行規格、設計及材質之列表比較，並針對差異處進評估。 2. 生物相容性評估 (Biocompatibility) 依據產品與人體接觸之性質與時間，進行風險評估：
豁免機制：若採用常用之醫用金屬（如 Ti6Al4V, 316L 不鏽鋼等）且製程未改變，得檢具材質證明申請豁免試驗。 執行標準：依據 ISO 10993 系列標準。重點評估項目包括細胞毒性、敏感試驗、刺激試驗、系統毒性、基因毒性及植入試驗。 3. 滅菌確效 (Sterilization) 無菌標準：無菌包裝產品之無菌保證水準 (Sterility Assurance Level, SAL) 必須符合 10⁻⁶。 滅菌驗證：須依據對應之 ISO 標準（如 17665-1, 11135 或 11137）提供滅菌計畫書與報告。對於非無菌提供之產品，應提供建議之醫事機構滅菌方法。 4. 機械性質評估 (Mechanical Testing) 機械測試應能模擬臨床最壞情況（Worst-case scenario）：
執行標準：建議參考 ASTM F1541。 評估項目： 剛性與屈折測量：評估固定器之結構穩定度。 靜態破壞測試：評估裝置在承受過負荷時之極限強度。 疲勞與鬆脫測試：模擬長期使用下之循環負荷，及接合處是否容易產生鬆動。 5. 特定風險與額外評估 (Special Risks and Additional Evaluations) 針對具備特殊宣稱或設計之產品，應額外提供資料：
脊椎或動態機能：若具備微動或動態機能，應提供相關動態功能測試報告。 MRI 相容性：若宣稱 MRI 安全（MRI Safe）或 MRI 條件（MRI Conditional），須依國際標準提交相關磁共振環境評估報告。 第二部分：骨外固定器查驗登記審查清單 (Review Checklist) 審查項目 審查重點 / 具備文件 審查結果 (符合/不適用/待補) 備註說明
1. 產品規格 1.1 用途說明 是否包含完整臨床適應症與適應對象？ □ 1.2 組件目錄 是否列出所有系統組件（錨定、橋接、接合器）？ □ 1.3 工程圖 主要組件是否具備詳細尺寸與標註？ □ 1.4 設計與組合 是否描述各組件之連接、鎖固機制？ □ 1.5 材質證明 是否提供材質證明並符合 ASTM/ISO 國際標準？ □ 1.6 等同性比較 是否與 Predicate Device 進行列表比較並評估差異？ □
2. 生物相容性 2.1 測試報告 是否依 ISO 10993 提供細胞毒性、過敏等基本報告？ □ 2.2 豁免說明 若申請豁免，是否提供符合常規金屬之佐證資料？ □
3. 滅菌確效 3.1 滅菌標準 無菌保證水準 (SAL) 是否符合 ≤ 10⁻⁶？ □ 3.2 驗證報告 是否提供符合 ISO 17665/11135/11137 之驗證資料？ □
4. 機械性質 4.1 剛性測試 是否提供符合 ASTM F1541 之剛性測量報告？ □ 4.2 靜態破壞 是否執行裝置整體之靜態破壞試驗？ □ 4.3 疲勞測試 是否針對組件間之疲勞與鬆脫進行評估？ □
5. 特定風險 5.1 動態機能 脊椎用或具動態功能者，是否提供風險評估或測試？ □ 5.2 結構硬度 若硬度低於市場類似品，是否有安全性合理說明？ □ 5.3 MRI 相容性 宣稱 MRI 相容者，是否提交環境相容性評估報告？ □ 審查結論： □ 建議核准 □ 需補件再議（補件項目：____________________） □ 不予核准

審查人員簽章： ____________________ 日期： 2026-03-13

























Hi please create a wow interactive webpage that 1. User can paste medical device regulation news, guidance/regulation/standard 2. User can paste description of skill (skill.md) (optional). 3. User can paste medical device regulations report template or use the default report template 4. User can select languages for output (English/traditional chinese (default)). 5. Agent will search web and create a comprehensive summary of the related medical device regulation/guidance of the step 1 user provided information in markdown in 2000~3000 words. 6. Agent will create a comprehensive medical device regulation report based on step 1 user provided information and step 5 comprehensive summary using the user provide report template or default template in markdown in 3000~4000 words. Agent will also create 4 wow Infograph (using code to be presented on interactive webpage) and also create 3 additional table, 20 entities with context based on the previous regulation report. Please also create 3 wow/amazing features (create by the agent) attached to the report. Ending with 20 comprehensive follow up questions. 7 Agent will create a description of skill to search the web and create a comprehensive medical device regulation report based on previous steps and combine step 2 user provided description of skill using the skill creator skill. Please add 3 additional wow features to this skill. 8 Agent will create a NEAT wow interactive webpage containing step 5, 6, 7 results using the user select language. User can choose light/dark themes, English/traditional chinese and 10 styles based on Pantone color palette within the webpage. Default report template: skill creator skill:

醫療器材法規全球協調化深度報告：加拿大 Health Canada REP 與美國 FDA QMSR 實施全指南
一、 前言：全球醫療器材監管的數位化與標準化浪潮
在 2024 年至 2026 年間，全球兩大重要醫療器材市場——加拿大與美國——正經歷一場前所未有的法規範式轉移。加拿大衛生部（Health Canada）推動的「法規註冊流程（Regulatory Enrolment Process, REP）」以及美國食品藥物管理局（FDA）發布的「品質管理體系法規（Quality Management System Regulation, QMSR）」，共同標誌著醫療器材產業進入了「數位化申報」與「國際標準接軌」的新紀元。
本報告旨在深度解析這兩項重大變革。Health Canada 的 REP 透過網路化模板與自動化系統提升了審查效率；而美國 FDA 的 QMSR 則透過引用 ISO 13485:2016，實現了與國際品質管理標準的高度統一。這兩項政策的強制實施日期均定於 2026 年上半年，這對全球醫療器材製造商而言，既是合規挑戰，也是優化企業內部管理體系的轉機。

二、 加拿大 Health Canada：法規註冊流程 (REP) 深度解析
1. REP 的核心概念與運作機制
加拿大衛生部的 REP 是一項跨業務線的共同收件流程。其核心在於捨棄傳統的紙本或非結構化電子表單，轉而採用「Web-based Templates（網頁式模板）」。
* 技術基礎： REP 透過「通用電子提交網關（Common Electronic Submission Gateway, CESG）」接收各類交易。
* 自動化導入： 系統能自動將廠商提交的元數據（Metadata）與交易資訊導入 Health Canada 的內部數據庫，極大減少了人工登錄錯誤。
* 範疇擴展： 雖然最初是針對藥品開發，但目前已全面擴散至醫療器材、生物製品及獸藥等領域。
2. REP 實施時程與強制性要求
根據官方公告，REP 的轉型採取了循序漸進的策略：
* 多年度試行階段： 經過長達數年的 Pilot 測試，確保系統穩定性。
* 自願使用期： 2024 年 7 月起，開放製造商自願選擇使用 REP 進行申報。
* 全面強制執行： 2026 年 4 月 1 日起，所有進入加拿大市場的醫療器材相關申請必須透過 REP 流程完成，不再接受傳統申報方式。
3. 製造商的具體獲益
採用 REP 流程，廠商可獲得以下顯著優勢：
* 即時數據驗證： 網頁模板具備自動檢核功能，若資料格式不符，系統會即時提醒，降低補件率。
* 生命週期管理： 製造商能更清晰地追蹤產品在 Health Canada 系統內的註冊狀態與過往交易記錄。
* 減少重複勞動： 透過結構化數據，許多企業資訊只需登錄一次，即可在多個申請案中重複引用。

三、 美國 FDA QMSR：從 21 CFR Part 820 到 ISO 13485 的接軌
1. 法規背景與核心轉變
美國 FDA 於 2024 年發布的最終規則（Final Rule），將原本的《品質體系法規（QSR）》修訂為《品質管理體系法規（QMSR）》。這項改革的核心是直接引用 ISO 13485:2016 作為 FDA 對製造商品質系統的基本要求。
這項變動解決了長期以來製造商必須同時滿足 FDA 專有標準與國際 ISO 標準的「雙重負擔」問題。QMSR 的生效日期定於 2026 年 2 月 2 日，屆時所有的檢查（Inspections）都將基於新的 QMSR 標準。
2. 法律效力與上市前申請 (PMA/HDE)
雖然 QMSR 大量引用 ISO 標準，但其背後的法源依據仍是美國《聯邦食品、藥物和化妝品法案》。對於高風險器材的「上市前核准申請（PMA）」或「人道主義器材豁免（HDE）」，FDA 要求必須在申請文件中包含品質系統的完整描述。若廠商提交的 QMS 資訊無法證明其符合現行優良製造規範（CGMP），FDA 有權拒絕核准。

四、 深度對標：ISO 13485 條款與 FDA 額外期待
在 QMSR 框架下，FDA 並非全盤照搬 ISO 13485，而是針對某些美國法律特有的要求進行了補充。以下為核心條款的深度解讀：
1. 風險管理（ISO 13485 Clause 4 & 7）
FDA 的 QMSR 強調「風險基準方法（Risk-based approach）」必須貫穿整個品質體系，而不僅僅是產品設計。製造商需解釋如何利用風險評估來決定委外流程的控制力道、軟體驗證的深度以及 CAPA 的優先順序。
2. 管理責任（ISO 13485 Clause 5）
FDA 依然保留對「管理代表」的重視。在提交 PMA 時，廠商必須明確識別管理代表，並提供管理審查（Management Review）的程序與摘要。這能確保高層管理者不僅僅是簽字，而是實質參與品質決策。
3. 環境與污染控制（ISO 13485 Clause 6.4）
對於無菌植入物，FDA 的要求比 ISO 13485 更具體。廠商需提交潔淨室（Cleanroom）的驗證數據、空氣潔淨度標準以及微生物控制流程。
4. 產品實現與設計控制（ISO 13485 Clause 7）
這是 FDA 上市前審查的重中之重。
* 設計確認（Design Validation）： 必須在「具代表性」的產品上進行。如果驗證產品與最終申報產品有差異，必須提供詳細的科學解釋。
* 設計轉移（Design Transfer）： 廠商需證明設計輸出已成功轉化為生產規範，這包括設備的安裝鑑定（IQ）、操作鑑定（OQ）及表現鑑定（PQ）。

五、 報告必備：關鍵對照表與數據分析
表格 1：Health Canada REP 與傳統申報模式對比
比較維度	傳統模式 (Legacy)	REP 模式 (Modernized)
收件管道	郵寄 CD/USB 或電子郵件	CESG 電子網關 (結構化傳輸)
資料格式	Word/PDF 靜態文件	XML/網頁動態模板
元數據 (Metadata)	人工提取，易出錯	自動導入 Health Canada 系統
處理效率	數週至數月 (含人工錄入)	即時/自動化數據確認
強制時間	2026 年 4 月 1 日淘汰	2026 年 4 月 1 日起唯一合法途徑
表格 2：FDA QMSR 對 ISO 13485 的主要補充要求
ISO 13485 條款	FDA QMSR 額外/特定要求 (21 CFR Part 820)	關鍵說明
不特定條款	唯一器材識別碼 (UDI)	必須符合 21 CFR Part 830 要求
Clause 8.2.1	醫療器材報告 (MDR)	必須符合 21 CFR Part 803，死亡或重傷需通報
Clause 8.3	矯正與移除 (Recalls)	必須符合 21 CFR Part 806 要求
Clause 4.2.4	記錄控制 (Record Control)	必須包含 UDI，且投訴記錄須具備特定美式格式
Clause 7.5.11	標籤與包裝控制	強化對標籤完整性檢查的程序要求 (820.45)
表格 3：2024-2026 跨國合規關鍵里程碑
日期	法規主體	事件性質	廠商應對行動
2024/02	美國 FDA	QMSR 最終規則發布	啟動與現有 QSR 的差異分析
2024/07	加拿大 HC	REP 開放自願使用	測試 CESG 帳號與網頁模板
2026/02/02	美國 FDA	QMSR 正式生效	



