# PharmaTrac AI — Presentation Script
### UiPath AgentHack 2026 | Track 1: Maestro Case | Presenter: Pugalesan I

---

## 🎬 Slide 1 — Title

> Hello judges, my name is Pugalesan, and today I am proud to present PharmaTrac AI — an autonomous, multi-agent pharmacovigilance and global recall control plane built on the UiPath Automation Cloud. PharmaTrac AI eliminates the manual, reactive safety loops in medicine distribution, replacing them with a secure, real-time safety control plane that bridges AI and human governance. Our system orchestrates **six distinct case stages** with **eight specialized agents**, all governed by Human-in-the-Loop decision gates.

---

## 🔥 Slide 2 — The Pharmacovigilance Bottleneck

> Every year, pharmaceutical companies face critical contamination crises. The warnings don't arrive in clean tables — they are hidden in unstructured emails, doctor notes, or portal forms. Because traditional automation relies on strict, rules-based logic, it is blind to this unstructured mess. Human safety officers are forced to manually sort and cross-reference thousands of clinical complaints against supply chain records. By the time a pattern is detected, weeks or months have passed, costing lives and exposing enterprises to massive liabilities.

---

## 🏗️ Slide 3 — Orchestrated by UiPath Maestro Case

> PharmaTrac AI solves this by coordinating a unified, state-driven case plan using UiPath Maestro Case. Rather than relying on isolated scripts, we modeled a BPMN 2.0 orchestration process divided into **six orchestrated stages**: **Received**, **Enriching**, **Cluster Analysis**, **Human Action**, **Recall Decision**, and **Closed**.
>
> Incoming narratives are validated against a strict schema, creating a live case record. After the Cluster Analysis stage detects a potential safety signal, the case enters the **Human Action stage** where a Safety Officer reviews all evidence through a custom UiPath App before the Recall Decision agent synthesizes the final recommendation.
>
> Maestro Case acts as our core governance plane, guiding the transaction data through specialized cognitive agents and human validation gates.

---

## 🧠 Slide 4 — Specialized Cognitive Agents

> At the heart of the system is a collaborative network of **eight specialized agents** built with UiPath Agent Builder and powered by Gemini 2.5 Flash.
>
> First, the **ComplaintIntelligenceAgent** digests the unstructured narrative to identify the product, batch ID, symptom, and extraction confidence.
>
> Second, the **BatchLookupAgent** enriches this payload by querying ERP logs to pinpoint the manufacturing facility and distribution network.
>
> Third, the **ClusterDetectionAgent** conducts cross-document reasoning — if multiple independent events trace back to the same batch or factory, it flags a cluster warning and drafts a diagnostic safety report.
>
> The case then enters the **Human Action** stage, where the EscalationApp presents all evidence to a Safety Officer for HITL review.
>
> After sign-off, the **RecallDecisionAgent** evaluates the final recall recommendation, and the **CaseClosureAgent** compiles the closure report with **Gmail alerts** sent to distributors via the UiPath Google Gmail Connector.

---

## 👤 Slide 5 — Human-in-the-Loop Governance

> Because pharmaceutical recalls carry massive weight, safety actions cannot be left entirely to AI models. PharmaTrac AI enforces a strict Human-in-the-Loop architecture through the dedicated **Human Action stage** — Stage 4 in our six-stage pipeline.
>
> If a cluster threat is flagged, Maestro Case pauses background processes and sends an urgent diagnostic task to a safety executive via a custom UiPath App called **EscalationApp_Final**. Inside this dashboard, the executive views the raw text, the extracted details, and the agent's reasoning. They can choose to **Initiate a Recall**, **Escalate to the Lab** for further investigation, or **Dismiss** the case.
>
> This decision then flows into **Stage 5 — Recall Decision** — where the RecallDecisionAgent synthesizes the final recommendation report before the case proceeds to closure.

---

## 🚀 Slide 6 — Impact, Resiliency & Future Scope

> In the event of an approved recall, the **RecallDecisionAgent** synthesizes the final recommendation, and the **CaseClosureAgent** compiles the complete case history into an auditable report. Background robots instantly run, freezing the toxic batch in the ERP, stopping distribution, and firing alerts to suppliers via the Google Gmail integration.
>
> Our **six-stage pipeline** with **eight specialized agents** demonstrates how enterprises can build, run, and govern agentic safety solutions at scale using UiPath Maestro Case Management and Human-in-the-Loop dashboards.
>
> Thank you for your time, and I look forward to your questions.

---

## 📊 Quick Reference

| Stage | Name | Key Activity |
|-------|------|-------------|
| 1 | Received | RPA Ingestion, Schema Validation, Duplicate Check |
| 2 | Enriching | LLM Parsing, Entity Extraction, Confidence Score |
| 3 | Cluster Analysis | Batch Lookup, Anomaly Detection, Safety Report |
| 4 | Human Action | EscalationApp, HITL Review, Officer Sign-off |
| 5 | Recall Decision | Decision Agent, Recall Report, Action Routing |
| 6 | Closed | Case Closure, Gmail Alerts, Case Archive |

| # | Agent | Role |
|---|-------|------|
| 1 | ComplaintIntelligenceAgent | Entity Extraction |
| 2 | BatchLookupAgent | ERP Enrichment |
| 3 | ClusterDetectionAgent | Anomaly Detection |
| 4 | EscalationApp_Final (HITL) | Human Review |
| 5 | RecallDecisionAgent | Recall Evaluation |
| 6 | CaseClosureAgent | Case Resolution |
| 7 | Gmail Integration | Alert & Notify |
| 8 | PharmaSignal_CaseTrigger | Ingestion RPA |
