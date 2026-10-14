# ChronoTrace: Hackathon Project Plan & Execution Guide

**Hackathon:** AIORI-3 Hackathon  
**Problem Statement:** PS-013: Incident Timeline and Evidence Collection for Small Teams  
**Team Code:** `A3-PS013-TC027`  
**Team Name:** Team H2RN  
**Lead:** Rachit Ingole (Vishwakarma Institute of Technology)  
**Team Intro Video:** [https://youtu.be/hBy8PVy-54U](https://youtu.be/hBy8PVy-54U)  

---

## 1. Executive Summary & Hackathon Mission

To build and demonstrate a working prototype of **ChronoTrace**—a lightweight, developer-friendly incident response platform tailored for small engineering teams. 

### What We Are Delivering in the Hackathon
1. **`chronoctl` (CLI Agent):** A zero-dependency script/binary that captures volatile evidence adhering to **RFC 3227 Order of Volatility** in under 30 seconds, hashes every artifact with SHA-256, and signs the manifest.
2. **ChronoTrace Core Backend (FastAPI + SQLite/DuckDB):** Ingestion endpoints for evidence bundles, webhook endpoints for external triggers (GitHub, Slack, Syslog), UTC timestamp normalization, and an immutable evidence vault.
3. **ChronoTrace Web UI (Modern Interactive Dashboard):** An interactive multi-track visual timeline showcasing:
   - System/Host Events & volatile snapshots
   - Alert notifications (Sentry/CloudWatch)
   - Responder actions & terminal command logs
   - Code changes & deployment commits
4. **Automated Evidence Vault & Chain of Custody Viewer:** Interactive inspection of all captured artifacts with verifiable SHA-256 integrity checks.
5. **1-Click AI Incident Post-Mortem & CERT-In 6-Hour Reporting:** Automated synthesis of a full blameless post-mortem markdown document and pre-filled CERT-In reporting form.
6. **Live End-to-End Incident Simulation Demo:** A simulated server intrusion script showing real-time detection, collection, timeline reconstruction, and report generation in under 2 minutes.

---

## 2. Team Work Breakdown Structure (WBS)

For Team H2RN, tasks are divided into 4 parallel tracks:

| Track | Primary Responsibilities | Deliverables |
| :--- | :--- | :--- |
| **Track 1: CLI Agent & Triage Engine** (`chronoctl`) | Evidence harvesting scripts, RFC 3227 order of volatility implementation, SHA-256 hashing, packaging, system commands (`ss`, `ps`, `lsof`, `journalctl`). | `chronoctl.py` or `chronoctl.sh`, test fixtures, CLI upload client. |
| **Track 2: Backend API & Vault** | FastAPI server, schema models, SQLite/DuckDB database, webhook receivers, UTC normalization logic, evidence vault storage, zip verification. | REST API endpoints (`/api/incidents`, `/api/collect`, `/api/timeline`, `/api/evidence`). |
| **Track 3: Frontend Dashboard & Timeline UI** | Modern web dashboard, multi-track timeline visualization (vis.js or custom SVG/CSS timeline), interactive filters, evidence viewer modal. | Responsive, sleek web UI running on Vite/React or lightweight frontend. |
| **Track 4: Reporting, AI Scribe & Demo Simulation** | Incident simulator script (mock breach scenario), AI post-mortem synthesis prompt/engine, CERT-In compliance export template, presentation slides. | `simulate_incident.py`, `post_mortem_generator.py`, slide deck based on PDF structure. |

---

## 3. Detailed Milestone Schedule (Hackathon Timeline)

### Phase 1: Foundation & Core Scaffolding (Hours 0 – 8)
- [x] Deep research of RFC 3227, ISO/IEC 27037, NIST SP 800-61, and CERT-In compliance mandates.
- [x] Author comprehensive project architecture (`IDEA.md`).
- [ ] Initialize repository structure:
  - `src/agent/` (`chronoctl`)
  - `src/backend/` (FastAPI, database models, timeline service)
  - `src/frontend/` (Dashboard, timeline visualizer)
  - `src/simulator/` (Mock attack scenario script)
  - `docs/` (Presentation & architecture diagrams)
- [ ] Develop `chronoctl` prototype to gather:
  - Active network connections (`ss -tulpen` or `netstat`)
  - Process tree with PIDs and CLI arguments
  - Recent auth logs / system journal
  - Host metadata and environment variables
  - Compute SHA-256 for all collected files and output `manifest.json`.

### Phase 2: Ingestion, Database & Evidence Vault (Hours 8 – 18)
- [ ] Implement FastAPI backend:
  - `POST /api/incidents`: Create/manage incident contexts (e.g. `INC-2026-001`).
  - `POST /api/incidents/{id}/evidence`: Accept zipped evidence bundle, verify SHA-256 checksums against manifest, store in immutable vault.
  - `POST /api/incidents/{id}/events`: Generic webhook endpoint for external event logs (GitHub commits, Slack notes, Sentry errors).
- [ ] Implement UTC Time-Sync Normalizer:
  - Converts all timestamps to ISO 8601 UTC.
  - Auto-assigns incident phases: *Trigger*, *Detection*, *Triage*, *Containment*, *Recovery*.
- [ ] Store incident events and evidence records in SQLite database.

### Phase 3: Interactive Visual Timeline & UI Dashboard (Hours 18 – 28)
- [ ] Build the ChronoTrace Web UI:
  - **Overview Header:** Incident Title, Severity Badge, Status (Active/Contained/Closed), MTTA & MTTR metrics.
  - **Multi-Track Interactive Timeline:** Visual swimlanes separating:
    - *Track 1: Monitoring & Alerts*
    - *Track 2: Host Telemetry & Artifact Dumps*
    - *Track 3: Human Decisions & Operator Scribe*
    - *Track 4: CI/CD & Deployments*
  - **Evidence Vault Inspector:** Table of collected files, file size, SHA-256 hash, download button, and integrity verification badge (green check for matching hash).
  - **Manual Event Ingestion Form:** Allows responders to quickly add key manual actions ("Isolated VM at 22:15 UTC").

### Phase 4: AI Post-Mortem, Compliance Export & Simulation (Hours 28 – 38)
- [ ] Implement automated report generation:
  - **Blameless Post-Mortem Generator:** Markdown document containing Executive Summary, Timeline, Root Cause, Impact, What went well / wrong, and Action items.
  - **CERT-In 6-Hour Reporting Template:** Pre-filled incident notice format required under Indian regulations.
- [ ] Build realistic simulated intrusion scenario (`simulate_incident.py`):
  1. Unauthorized SSH brute-force attempt logged in `/var/log/auth.log`.
  2. Malicious reverse shell script spawned in `/tmp/sh_rev`.
  3. Outbound connection established to external C2 IP.
  4. Sentry/alert fires.
  5. Operator triggers `chronoctl collect`.
  6. Operator contains incident (`kill` process, block IP).
  7. ChronoTrace reconstructs the entire sequence automatically.

### Phase 5: Testing, Polish & Pitch Presentation (Hours 38 – 48)
- [ ] Polish UI aesthetics (dark mode, clean typography, responsive layout).
- [ ] Prepare slide deck adhering directly to `Proposed-structure-hackathon.pdf`:
  - Slide 1: Cover (Team Code: `A3-PS013-TC027`, Team H2RN, Rachit Ingole)
  - Slide 2: Abstract & Problem Description
  - Slide 3: Background & Small Team Pain Points
  - Slide 4: Literature & RFC Review (RFC 3227, ISO/IEC 27037, CERT-In)
  - Slide 5: Proposed Solution (ChronoTrace Platform)
  - Slide 6: Solution Optimization (Before vs After comparison)
  - Slide 7: Architecture Design (UML & System Diagrams)
  - Slide 8: Data Flow Diagram (DFD Level 0 & Level 1)
  - Slide 9: Deployment Timeline & Project Plan
  - Slide 10: Bibliography & Standards
  - Slide 11: Conclusion & Q&A
- [ ] Rehearse 3-minute winning demo video/pitch.

---

## 4. Key Hackathon Judging Criteria & How ChronoTrace Wins

| Judging Criteria | Standard Hackathon Entry | ChronoTrace Strategy (Winning Edge) |
| :--- | :--- | :--- |
| **Problem Relevance & Innovation** | Generic logging dashboard or basic Slack bot. | Solves real pain point for small teams with strict RFC 3227 order-of-volatility evidence capture and 6-hour CERT-In compliance. |
| **Technical Depth** | Simple CRUD web app. | Forensic-grade SHA-256 hashing, immutable evidence vault, multi-track time-sync normalization, and AI causal correlation. |
| **Standards Compliance** | No RFC grounding. | Direct implementation of **RFC 3227, ISO/IEC 27037, RFC 5424, and CERT-In Direction 20(1)**. |
| **Feasibility & Usability** | Complex setup requiring dozens of microservices. | Zero-dependency 1-command deployment (`chronoctl` + lightweight containerized backend). Small teams can deploy it in 2 minutes. |
| **Live Demonstration** | Mocked screenshots or static tables. | Live, interactive simulated breach triage: trigger exploit -> automated collection -> instant timeline generation -> one-click export. |

---

## 5. Next Steps for Development

1. Review and validate `IDEA.md` and `PROJECT_PLAN.md`.
2. Commit and push documents to GitHub repository (`https://github.com/Rachit-Ingole/A3-PS013-TC027`).
3. Scaffold the `src/` codebase with backend, agent, and frontend directories.
