# ChronoTrace ⏱️🛡️

> **Incident Timeline & Cryptographic Evidence Vault for Small Teams**  
> *AIORI-3 Hackathon* • **Team Code:** `A3-PS013-TC027` • **Team Name:** Team H2RN  
> **Problem Statement:** PS-013 — Incident Timeline and Evidence Collection for Small Teams

---

## 🎥 Team Introduction Video
* **Video Link:** [https://youtu.be/hBy8PVy-54U](https://youtu.be/hBy8PVy-54U)

---

## 👥 Team Information (Team H2RN)
* **Team Code:** `A3-PS013-TC027`
* **Institute:** Vishwakarma Institute of Technology (VIT), Pune
* **Team Lead:** Rachit Ingole
* **Track Division & Responsibilities:**
  * **Track 1 (CLI Agent & Triage Engine):** `chronoctl` zero-dependency volatile evidence collection adhering to RFC 3227.
  * **Track 2 (Backend API & Vault):** FastAPI ingestion microservice, multi-source UTC time normalizer, and SHA-256 cryptographic evidence vault.
  * **Track 3 (Frontend UI & Visual Timeline):** Interactive multi-track incident timeline dashboard with swimlanes.
  * **Track 4 (AI Scribe & Compliance):** Automated blameless post-mortem synthesis and statutory CERT-In 6-hour incident report generator.

---

## 💡 About ChronoTrace
Small engineering teams lack dedicated Security Operations Centers (SOCs) or specialized forensics personnel. During production outages, engineers prioritize rapid recovery (restarting services or rebooting VMs), accidentally destroying critical in-memory evidence and violating the **RFC 3227 Order of Volatility**.

**ChronoTrace** solves this with:
1. **One-Command Live Triage (`chronoctl`):** Captures volatile memory, open network sockets, process trees, and auth logs in under 30 seconds.
2. **Cryptographic Chain of Custody:** Calculates SHA-256 hashes for all collected artifacts and seals them in a tamper-evident vault.
3. **Unified UTC Timeline:** Ingests host telemetry, AWS CloudWatch, Docker logs, GitHub commits, and Sentry alerts into a normalized timeline.
4. **AI Incident Scribe & CERT-In Compliance:** Automatically generates blameless post-mortems and pre-filled reports for the Indian CERT-In 6-hour disclosure mandate.

---

## 📁 Repository Structure
* `src/agent/`: `chronoctl` lightweight evidence harvester script
* `src/backend/`: FastAPI backend, ingestion pipeline, and database models
* `src/frontend/`: Interactive incident dashboard and multi-track visual timeline
* `docs/`: Presentation decks, architecture diagrams, and RFC review
* `IDEA.md`: Comprehensive technical specification and system architecture
* `PROJECT_PLAN.md`: Work breakdown structure, milestones, and deliverables
