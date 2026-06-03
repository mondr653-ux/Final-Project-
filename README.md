# 🥦 QR-Code Food Safety Information System — Final Project

**Team RJ:** Raymond Xu, Jihan Yang
**Course:** IMT 542 — Information Structures & Access

A portable, QR-code–based food safety system that lets consumers, suppliers, retailers, and regulators scan a food product and instantly retrieve structured safety, recall, origin, and supply-chain information. The project extends the **GS1 Digital Link** standard, follows the **FAIR** data principles, and is built to run in **Google Colab** with a JSON-based portable information structure.

---

## 📂 Repository Contents

This repository brings together every stage of the project — from the original product concept, through the information-structure design and FAIR/portability analysis, to the working prototype, dashboard, and test plan. Each file below has its own short introduction.

---

### 📊 G2 — Food Inspection & Management 
This file is the project's foundational concept document, captured as a CSV. It defines the product — a *Food Safety Inspection & Management System* — along with its purpose, target beneficiaries, and intended impact. It outlines who the system serves (ordinary consumers, families, people with food allergies, patients with chronic conditions, the elderly, schools, hospitals, producers, and regulators) and lays out the three core product directions: a QR-label scanner for food traceability, a standardized color-based food safety rating system, and a food-health mobile app with alerts and recall notifications. This document anchors the rest of the project by establishing the problem space and the value proposition.

---

### 📱 G4 — FoodSpy App Concept & Architecture 
This is the product concept and system-architecture deck for **FoodSpy**, the mobile food-inspection app. It describes the five core user actions (scan a QR code, check food source and processing, check additives and health score, receive recall alerts, and view company information) and presents the underlying data architecture. The deck includes the **controlled vocabulary** (e.g., `product_id`, `origin_location`, `processing_steps`, `additive_list`, `safety_rating`, `recall_status`) and the **derived/calculated data** fields (`health_score`, `risk_level`, `transparency_score`). It also defines the basic system architecture — batch regulatory datasets, real-time consumer scans, and external recall APIs — and the data flow: *Scan → product_id → retrieve data → generate insights → display.*

---

### 🔗 G5 — FAIR Model Analysis 
This document evaluates the food safety information structure against the **FAIR principles** (Findable, Accessible, Interoperable, Reusable). It explains how each product or batch receives a unique `product_id`/`batch_id` linked to a QR code with descriptive metadata (Findability); how consumers retrieve information through a standard web/app interface while sensitive data stays behind authentication (Accessibility); how the structured JSON format with consistent fields enables data exchange between companies, regulators, and consumer apps (Interoperability); and how provenance tracking — origin, who updated a record, inspection timing, and data source — supports reuse (Reusability). It also honestly notes the gaps still to close: a clearer data-usage license and stronger food-safety standards.

---

### 🧱 G7 — Improved Information Structure 
This file documents the heart of the project: the redesign of the information structure. It first shows the **existing** GS1 Digital Link structure and its limitations (no origin location, no processing steps, no inspection status, no recall status, no access control, no change log). It then presents the **improved** structure — the *QR-Code-Based Food Safety Record* — a hierarchical JSON schema that extends GS1 with `record_metadata`, `product_identifier`, `supply_chain_information` (including step-by-step processing history), `safety_and_quality_information`, `recall_information`, and `system_and_security_metadata` with role-based public/private access control and audit tracking. This is the canonical schema that the prototype and dashboard are built around.

---

### 📖 G8 — QR-Code Food Safety Inspector API 
This is the API design and documentation for the system. It describes the API's purpose and audience, the methodology for aggregating data from supplier databases, state inspection records, and federal recall feeds, and the role-based access model. A key section covers the **technical mechanisms to prevent misinformation** through three trust pillars: cryptographic digital signatures (an electronic seal that invalidates tampered records), live API oracles that cross-reference official government databases in real time, and GS1 Digital Link domain verification. The document includes the access flow for consumers vs. regulators, the nested JSON structure, and a worked example request/response showing how `consumer_access_view` filters out sensitive backend fields.

---

### ✅ G9 — Test Plan 
This is the quality-control and reliability test plan for the system. It defines quality objectives (accuracy, availability, performance, portability, security/privacy, traceability) and provides detailed test matrices for functional testing, data-quality testing, and performance/load testing. It also specifies alarms and monitoring triggers (API down, high latency, stale recall data, schema-validation failures, unauthorized access attempts) with their corresponding actions, plus an ongoing implementation plan covering development, pre-release checks, continuous CI/CD testing, and scheduled monitoring. It closes with team responsibilities and a roadmap of future testing additions.

---

### 🎓 IMT542 FINAL — Final Project Submission
This is the consolidated final deliverable for the IMT 542 course, bringing together the complete body of work: the problem definition, the existing-vs-improved information structure analysis, the FAIR and portability evaluations, the API design, the working prototype, the dashboard, and the test plan. It serves as the capstone summary that ties every component of the repository into a single, coherent project narrative.

---

### 🏷️ Portable GS1 — Baseline Reference Structure 
This file captures the **starting point** for the whole project: the standard **GS1 Digital Link** structure as it exists today. It documents the URI format encoded in the QR code, the parsed identifiers (GTIN, batch/lot number, expiration date), and the linked web resources (product landing, traceability, and nutrition pages). Crucially, it records the **observed limitations** for this project — the fields GS1 does *not* provide, such as origin location, processing facility, inspection status, recall status, verification status, access control, and change log. These documented gaps are exactly what the improved structure (G7) was designed to fill.

---

### 🐍 Project: Portable_info_QR.ipynb
This is the working **Google Colab prototype** of the system. The notebook includes an *Open in Colab* badge, file-upload support, and a `FoodSafetySystem` class that generates QR codes for food products using the improved JSON schema. It builds sample product records, generates scannable QR codes, renders the food safety dashboard inline, and runs quality checks and a performance benchmark (timing 1,000 consumer-view lookups across the product set). This notebook is the runnable heart of the project — open it in Colab to generate QR codes and explore product records end-to-end.

> **To run:** Open the notebook, upload `export_all_products.json` and `food_safety_dashboard.html` when prompted, then run the cells in order.

---

### 🖥️ food_safety_dashboard.html
This is the consumer-facing **dashboard** that renders product safety information in a clean, mobile-friendly layout. It displays product identity, expiration status, inspection results, origin and processing chain, allergens, nutrition, and any active recall alerts as visual cards. It can be opened directly in a browser or rendered inline inside the Colab notebook, giving consumers an at-a-glance, easy-to-read view of whether a scanned product is safe.

---

### 🌐 index.html
This is the main entry-point web page for the project — the landing page that ties the system together and provides access to the dashboard and product lookup. It serves as the front door for users opening the project as a website, presenting the food safety system in a browser-ready interface.

---

## 🚀 Quick Start

1. **Open the prototype:** Click the *Open in Colab* badge in `Project: Portable_info_QR.ipynb`.
2. **Upload supporting files** when prompted: `export_all_products.json` and `food_safety_dashboard.html`.
3. **Run all cells** to generate QR codes, view product records, and render the dashboard.
4. **Explore the design:** Read `Portable GS1` (baseline) → `G7` (improved structure) → `G5 FAIR model` (principles) → `G8 API` (access design) → `G9 Test Plan` (quality).

---

## 🧩 How the Pieces Fit Together

| Stage | File(s) | What it answers |
|---|---|---|
| Concept | G2, G4 | What are we building and for whom? |
| Baseline | Portable GS1 | What does the existing standard offer — and lack? |
| Redesign | G7 | How do we improve the information structure? |
| Principles | G5 FAIR model | Is the structure findable, accessible, interoperable, reusable? |
| Access & trust | G8 API | How do users retrieve data, and how do we prevent misinformation? |
| Quality | G9 Test Plan | How do we know it works and stays reliable? |
| Prototype | Portable_info_QR.ipynb | A runnable demo |
| Interface | food_safety_dashboard.html, index.html | What the user sees |
| Capstone | IMT542 FINAL | The full project, assembled |

---

*Built for IMT 542 by Team RJ — Raymond Xu & Jihan Yang.*
