# PharmaSignal AI 🩺📊
### *Enterprise-Grade Adverse Drug Event (ADE) Detection & Automated Recall Orchestration*
#### **Winner-ready Submission for UiPath AgentHack 2026 (Track 1: UiPath Maestro Case)**

---

## 🏆 Executive Summary

Pharmaceutical safety monitoring (Pharmacovigilance) is plagued by manual delays, fragmented systems, and slow reporting channels. When an Adverse Drug Event (ADE) occurs, it takes weeks or months of manual review to detect a batch-level defect cluster, risking patient lives and costing billions in legal, regulatory, and operational liabilities.

**PharmaSignal AI** is an enterprise-grade agentic case management system that reduces the time-to-detect safety clusters from **weeks to seconds**. Built entirely on **UiPath Automation Cloud**, it orchestrates API-driven triggers, cognitive LLM agents, historical database lookups, statistical safety rules, and rich human-in-the-loop validation dashboards. 

By keeping **Humans in the Loop (HITL)** for high-stakes recall decisions while automating extraction, enrichment, and analysis, PharmaSignal AI showcases how the AI agents of tomorrow operate, fail safe, and govern enterprise processes at scale.

---

## 💎 The 1st-Prize Value Proposition (Judging Criteria Alignment)

| Criteria | How PharmaSignal AI Delivers |
| :--- | :--- |
| **Business Impact & Adoption Potential** | Targets a multi-billion dollar compliance and safety bottleneck in pharma. Integrates directly with existing ERPs, complaints databases, and regulatory systems. Scalable to millions of complaints. |
| **Platform Usage** | Deep orchestration: combines **UiPath Maestro Case**, **Agent Builder**, **UiPath Apps** (for HITL), **Gmail Connectors**, and custom triggers into a unified enterprise control plane. |
| **Technical Execution & Feasibility** | Implements automated schema validations, confidence threshold safeguards, automatic escalation rules, and robust transaction state boundaries. |
| **Creativity & Innovation** | Leverages a dynamic agentic pipeline where the output of one LLM agent forms the context for lookup and statistical reasoning agents, culminating in a synthesized report for human sign-off. |
| **Coding Agents Bonus** | Developed and structured using AI coding agents (**Gemini CLI** and **Claude Code**) to design schemas, format bindings, and build validation test suites. |

---

## 🏗️ Architecture & Flow Control

The workflow is orchestrated via **UiPath Maestro Case** using a structured, state-driven case plan ([caseplan.json](PharmaComplaintCase/caseplan.json)) containing five distinct stages:

```mermaid
flowchart TD
    subgraph Stage 1: Received
        A[Incoming Complaint Narrative] --> B[PharmaSignal_CaseTrigger RPA]
        B --> C[Validate JSON Payload & Open Case]
    </td>

    subgraph Stage 2: Enriching
        C --> D[Complaint Intelligence Agent]
        D -->|Extracts symptoms, severity, batch IDs| E[Evaluate Confidence Score]
    end

    subgraph Stage 3: Cluster Analysis
        E -->|Confidence >= 80%| F[Batch Lookup Agent]
        E -->|Confidence < 80%| F_Esc[Flag High Risk/Low Confidence]
        F --> G[Cluster Detection Agent]
        G -->|Cross-Reference Historical Data| H[Synthesize Safety Report]
    end

    subgraph Stage 4: Recall Decision
        H --> I[Task: Escalation Review]
        I --> J[UiPath Interactive App: EscalationApp_Final]
        K((Safety Officer Sign-off)) -->|Interactive Review| J
    end

    subgraph Stage 5: Closed
        J -->|Decision: Initiate Recall| L[Recall Action Agent]
        J -->|Decision: Archive| M[Archive Case]
        L --> N[Send Alerts via Gmail Integration]
        M --> O[Generate Case Closure Summary]
        N --> P[Case Resolved & Archived]
        O --> P
    end

    style K fill:#ff9999,stroke:#333,stroke-width:2px
    style J fill:#b3d9ff,stroke:#333,stroke-width:2px
```

---

## 🧠 Dynamic Agent Roles & Technical Specifications

Each agent in the pipeline is built to handle specific enterprise operations:

### 1. Ingestion: `PharmaSignal_CaseTrigger`
* **Trigger Type**: API / Webhook Event.
* **Input Schema**: Validated against [PharmaSignal_Intake.json](../PharmaSignal_Intake/PharmaSignal_Intake.json) (requires `complaint_id`, `source_channel`, and `complaint_text`).
* **Function**: Sanitizes narrative text, checks for duplicates, creates a case record in Maestro Case, and transitions the case to the `Received` state.

### 2. Entity Extraction: `ComplaintIntelligenceAgent`
* **Core Logic**: LLM Cognitive Model.
* **Input**: Raw text narrative.
* **Outputs**: Product Name, Batch ID, Symptom Category, Severity, and Extraction Confidence.
* **Resiliency Safeguard**: If confidence is below 80% or if critical parameters (e.g., Batch ID) are missing, the agent flags `requires_human_review = true` to bypass normal execution and fast-track to manual review.

### 3. ERP Enrichment: `BatchLookupAgent`
* **Core Logic**: RPA Integration.
* **Input**: Product Name, Batch ID.
* **Function**: Queries internal manufacturing databases to identify the active manufacturing facility, distribution geography, and matches past complaints associated with that specific batch.

### 4. Anomaly Detection: `ClusterDetectionAgent`
* **Core Logic**: LLM reasoning combined with threshold check rules.
* **Inputs**: Current complaint symptoms, batch ID, history of matching complaints.
* **Evaluation Rules**: Calculates if complaints for a single batch exceed a safety coefficient (e.g., >3 events of identical symptom categories).
* **Outputs**: `cluster_detected` (Boolean), `signal_strength` (Low/Medium/High), and detailed text reasoning explaining the safety risk.

### 5. HITL Panel: `EscalationApp_Final` (UiPath App)
* **Design File**: [EscalationApp_Final.json](resources/solution_folder/app/vB%20Action/EscalationApp_Final.json).
* **UI Features**: Renders a dark-themed, glassmorphic executive screen displaying extraction data side-by-side with raw complaint records, the calculated cluster reasoning, signal strength, and a decision action panel (Initiate Recall, Escalate to Lab, Dismiss).

### 6. Action & Notifications: `RecallActionAgent`
* **Core Logic**: API Integration & Orchestration.
* **Function**: In the event of a "Recall" decision, compiles the case history into a report, updates safety records, and calls the **UiPath Google Gmail Connector** to send urgent alerts to distributor lists.

---

## 🛠️ Resiliency & Exception Handling (Failsafe Systems)

Production-ready software must survive real-world chaos. PharmaSignal AI incorporates multiple error boundaries:
* **Missing Batch IDs**: If the text doesn't contain a batch ID, the system queries the customer registry and distribution history to attempt auto-reconciliation. If it fails, it prompts a human analyst to fill the field.
* **System Outages**: If the ERP database is unreachable during the `BatchLookup` step, the system uses a cached fallback schema state and logs a warning task, allowing the safety case to proceed without halting.
* **Network & Token Limits**: Agent reasoning pipelines implement exponential backoff retry policies for OpenAI/Anthropic LLM API calls.

---

## 🚀 Step-by-Step Installation & Deployment

### 📋 Prerequisites
1. **UiPath Automation Cloud** tenant with **Maestro Case Management** enabled.
2. **UiPath Apps** service activated on the tenant.
3. **Google Gmail Connection** established in Integration Service.
4. **UiPath Studio** (v2023.10 or higher) with Case Management activities package.

### 🛠️ Execution Setup
1. **Clone project repository**:
   ```bash
   git clone <your-repository-url>
   ```
2. **Import Solution Package**:
   * Open UiPath Studio, click **Open**, and select [PharmaComplaintLast.uipx](PharmaComplaintLast.uipx).
   * Resolve any missing dependencies using the Nuget package manager.
3. **Configure Integration Connectors**:
   * Open **Integration Service** in your Automation Cloud tenant.
   * Verify that the Gmail connection `637f7779-bd13-41ab-b17a-15947b80ee2d` mapped in [bindings_v2.json](PharmaComplaintCase/bindings_v2.json) is active.
4. **Publish Case & App Templates**:
   * Publish the `PharmaComplaintCase` to the orchestrator folder of choice.
   * Import [EscalationApp_Final.json](resources/solution_folder/app/vB%20Action/EscalationApp_Final.json) inside **UiPath Apps** and link it to the Case Orchestrator queue.

---

## ⚖️ Licensing
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
