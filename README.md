# Food Ordering Behaviour & Customer Trends
### A Structured Analysis of Choices and Habits

A Tableau-based analytics project that transforms a 50,000-record food ordering dataset into an interactive, publicly shareable dashboard and story, surfacing insights on customer choices, ordering habits, and delivery performance.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Project Details](#project-details)
- [Dataset](#dataset)
- [Architecture / Technology Stack](#architecture--technology-stack)
- [Data Flow](#data-flow)
- [Functional Requirements](#functional-requirements)
- [Non-Functional Requirements](#non-functional-requirements)
- [User Stories](#user-stories)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Publishing the Dashboard](#publishing-the-dashboard)
- [Security & Privacy](#security--privacy)
- [Roadmap / Future Scope](#roadmap--future-scope)
- [Source Code](#source-code)
- [Dataset Link](#dataset-link)
- [GitHub & Project Demo Links](#github--project-demo-links)
- [Documentation](#documentation)

---

## Project Overview

This project analyzes food ordering behaviour and customer trends using a structured, end-to-end analytics pipeline. Raw order data is imported, cleaned, and enriched, then visualized in Tableau Desktop as a set of worksheets, assembled into an interactive dashboard, sequenced into a narrative story, and finally published to **Tableau Public** for open, read-only access.

The goal is to help business analysts, restaurant partners, and executives understand:

- What and how customers order (cuisine, meal type, company type)
- When and where orders happen (city, delivery time)
- How customers rate their experience
- Revenue and repeat-order patterns across segments

## Project Details

| Field | Value |
|---|---|
| Project Name | Food Ordering Behaviour & Customer Trends: A Structured Analysis of Choices and Habits |
| Phase | Project Design Phase – II |
| Team | Individual Submission |
| Primary Tool | Tableau Desktop / Tableau Public |
| Dataset Size | 50,000 records × 19 fields |

## Dataset

- **File:** `food_ordering_behavior_dataset.csv`
- **Size:** 50,000 records, 19 fields
- **Format:** Flat-file CSV
- Fields cover order details, customer demographics, cuisine/meal type, city, rating, delivery time, and company type (alone/family/friends/partner), among others.

> The schema (19 fields, correct data types) is validated as part of the extraction step before any analysis is performed.

## Architecture / Technology Stack

Rather than a multi-tier application backend, this project uses a lightweight **five-stage analytics pipeline**: a flat-file dataset → a lightweight preparation step → Tableau Desktop as the visualization engine → an assembled dashboard/story → Tableau Public as the hosting/publishing layer.

```
CSV Dataset  →  Data Prep  →  Tableau Desktop  →  Dashboard & Story  →  Tableau Public
(Source Data)  (Excel /       (Worksheets,        (Assembled)          (Publish)
                Tableau Prep)   Calc Fields)
```

### Table 1 — Components & Technologies

| # | Component | Description | Technology |
|---|---|---|---|
| 1 | Data Source / User Interface | How the business user interacts with the analysis | Tableau Dashboard, Tableau Story, Tableau Public (Web) |
| 2 | Data Extraction Logic | Reading and validating the raw order dataset | Python / Pandas (pre-analysis), CSV |
| 3 | Data Preparation Logic | Cleaning, type casting, derived fields (age group, revenue, repeat-order flag) | Tableau Data Prep / Excel |
| 4 | Visualization Logic | Calculated fields, worksheets, aggregations | Tableau Desktop (Calculated Fields, LOD Expressions) |
| 5 | Database | Underlying dataset | Flat-file CSV (50,000 rows × 19 columns) |
| 6 | Cloud Database | Extract storage for fast querying | Tableau Hyper Extract (.hyper) |
| 7 | File Storage | Workbook & data source storage | Packaged Tableau Workbook (.twbx), Local filesystem |
| 8–9 | External APIs | Not applicable — self-contained dataset | N/A |
| 10 | Machine Learning Model | Not used in this phase | N/A (future scope) |
| 11 | Infrastructure | Local build, cloud publish | Local Desktop + Tableau Public Cloud |

### Table 2 — Application Characteristics

| # | Characteristic | Description | Technology |
|---|---|---|---|
| 1 | Open-Source Frameworks | Pandas/Python used only for initial exploration; core visualization native to Tableau | Python, Pandas |
| 2 | Security | Read-only public view; only anonymised `order_id`/`user_id` retained | Tableau Public view-only permissions |
| 3 | Scalable Architecture | Extract-based (.hyper) design scales to more cities/years/rows | Tableau Hyper Extract Engine |
| 4 | Availability | Hosted on Tableau Public's cloud infrastructure | Tableau Public Cloud Hosting |
| 5 | Performance | Pre-computed aggregations render full dataset in under 5 seconds | Tableau Hyper Engine |

## Data Flow

**Level 0 (Context):** `External Source (Order Log CSV, 50,000 records)` → *raw order data* → `Food Ordering Behaviour Analytics System` → *dashboard & story* → `Business Users (Analysts, Restaurant Partners, Management)`

**Level 1 (Detailed):**

```
Order Log CSV Source
        │
        ▼
1.0 Data Extraction & Validation
        │
        ▼
2.0 Data Cleaning & Preparation ───► D1: Cleaned Dataset Store
        │
        ▼
3.0 Build Calculated Fields & Worksheets ◄──── insights ──── Business Users
        │
        ▼
4.0 Assemble Dashboard & Story
        │
        ▼
5.0 Publish to Tableau Public ──── publish link ────► Business Users
```

## Functional Requirements

| ID | Requirement (Epic) | Sub-Tasks |
|---|---|---|
| FR-1 | Data Collection & Extraction | Import CSV (50,000 records); validate schema (19 fields, correct types) |
| FR-2 | Data Preparation | Handle missing/duplicate records; create derived fields (age group, revenue, repeat-order flag) |
| FR-3 | Visualization Development | Build worksheets for KPIs, cuisine, meal type, city, rating, delivery time; create calculated fields |
| FR-4 | Dashboard Assembly | Combine worksheets into one dashboard; add quick filters and dashboard actions |
| FR-5 | Story Creation | Sequence dashboard views into a narrative; add guiding captions |
| FR-6 | Publishing | Publish workbook to Tableau Public; verify shareable public link |

## Non-Functional Requirements

| ID | Category | Description |
|---|---|---|
| NFR-1 | Usability | Intuitive filters, tooltips, and consistent color legends for non-technical users |
| NFR-2 | Security | Read-only public view; only anonymised `user_id` exposed, no PII |
| NFR-3 | Reliability | Consistent, repeatable results on every data refresh |
| NFR-4 | Performance | Renders in under 5 seconds for the full 50,000-record extract (Hyper engine) |
| NFR-5 | Availability | Hosted on Tableau Public, accessible 24/7 from any browser |
| NFR-6 | Scalability | Extract-based architecture scales to more cities, years, or records |

## User Stories

| User Type | Epic | ID | Story | Priority | Release |
|---|---|---|---|---|---|
| Business Analyst | Data Extraction & Preparation | USN-1 | Extract and validate the 50,000-record dataset before visualization | High | Sprint-1 |
| Business Analyst | Data Extraction & Preparation | USN-2 | View a KPI summary as soon as the dashboard opens | High | Sprint-1 |
| Business Analyst | Dashboard Filtering | USN-3 | Filter by city to see region-specific trends | High | Sprint-1 |
| Business Analyst | Dashboard Filtering | USN-4 | Filter by cuisine and meal type to compare preferences | Medium | Sprint-2 |
| Restaurant Partner | Segment Analysis | USN-5 | View order distribution by age group and segment | Medium | Sprint-2 |
| Restaurant Partner | Segment Analysis | USN-6 | See revenue contribution by meal type | High | Sprint-2 |
| Restaurant Partner | Rating & Delivery Insights | USN-7 | Review rating analysis by meal type | Medium | Sprint-3 |
| Business Executive | Behavioural Trends | USN-8 | View how company type affects order patterns | Medium | Sprint-3 |
| Business Executive | Behavioural Trends | USN-9 | See delivery-time distribution across orders | Medium | Sprint-3 |
| Business Executive | Story Narrative | USN-10 | Walk through a story sequencing dashboard views | High | Sprint-4 |
| Platform Administrator | Publishing | USN-11 | Publish the finished dashboard and story to Tableau Public | High | Sprint-4 |
| Platform Administrator | Publishing | USN-12 | Share the public link with stakeholders (read-only) | Low | Sprint-4 |

> Full acceptance criteria for each story are documented in `Data_Flow_Diagrams_and_User_Stories.docx`.

## Project Structure

```
├── 1. Ideation Phase/
│   ├── Brainstorming - Idea Prioritization.docx
│   ├── Define Problem Statements.docx
│   └── Empathy Map Canvas.docx
│
├── 2. Requirement Analysis/
│   ├── Data Flow Diagrams and User Stories.docx
│   ├── Data_Flow_Diagrams_and_User_Stories.pdf
│   ├── Solution Requirements.docx
│   ├── Solution_Requirements.pdf
│   ├── Technology Stack - Template.docx
│   └── Technology_Stack.pdf
│
├── 3. Project Design Phase/
│   ├── 2. Requirement Analysis/
│   ├── Problem - Solution Fit/
│   ├── Proposed Solution/
│   └── Solution Architecture/
│
├── 4. Project Planning Phase/
│   └── Project Planning.docx
│
├── 5. Project Development Phase/
│   ├── 1st PDF - Data Preprocessing & Business Understanding.docx
│   ├── 2nd PDF - Dashboard, Story & Public Link.docx
│   ├── 2nd PDF - Dashboard, Story & Public Link.pdf
│   └── food_ordering_behavior_dataset.csv
│
├── 6. Performance Testing Phase/
│
├── 7. Project Documentation/
│
└── README.md
```

> Folder names mirror the project's phase-wise submission structure (Ideation → Requirement Analysis → Design → Planning → Development → Performance Testing → Documentation), with each phase's deliverables (Word/PDF reports, the raw dataset, and the packaged Tableau workbook) kept together under the corresponding phase folder.

## Getting Started

1. **Prerequisites**
   - Tableau Desktop (any recent version with Hyper engine support)
   - (Optional) Python 3.x with `pandas` for pre-analysis/exploration
   - A [Tableau Public](https://public.tableau.com) account for publishing

2. **Load the data**
   - Open Tableau Desktop and connect to `food_ordering_behavior_dataset.csv`.
   - Confirm all 19 fields load with correct data types.

3. **Prepare the data**
   - Clean missing/duplicate records.
   - Create derived fields: age group, revenue, repeat-order flag.
   - (Optional) Use Python/Pandas for initial exploration before modeling in Tableau.

4. **Build the visualizations**
   - Create calculated fields for aggregations.
   - Build worksheets: KPI summary, cuisine, meal type, city, rating, delivery time.

5. **Assemble the dashboard**
   - Combine worksheets into a single interactive dashboard.
   - Add quick filters and dashboard actions for cross-filtering.

6. **Create the story**
   - Sequence dashboard views into a narrative storyboard.
   - Add captions guiding the viewer through key insights.

## Publishing the Dashboard

1. In Tableau Desktop, select **Server → Tableau Public → Save to Tableau Public As...**
2. Sign in with your Tableau Public account.
3. Publish the workbook (dashboard + story).
4. Verify the generated public link opens correctly and all filters/actions work for external viewers.
5. Share the read-only link with stakeholders.

## Security & Privacy

- The published workbook exposes **only an anonymised `user_id`** — no names, contact details, or payment information.
- The public view is **read-only**; external viewers can filter and explore but cannot edit or export raw data.
- No live external APIs are used — the solution is self-contained around the flat-file dataset.

## Roadmap / Future Scope

- Introduce a **machine learning model** for predictive insights (e.g., churn or demand forecasting) — not part of the current phase.
- Extend the data pipeline to support additional cities, years, or a larger record count via incremental refresh.
- Automate the extraction/validation step with a scheduled Python/Pandas job ahead of the Tableau extract refresh.

## Source Code

Data validation and pre-analysis exploration were performed using **Python (pandas)**; the core visualization, calculated fields, dashboard, and story were built **natively in Tableau Desktop**. No custom application source code was required, as this is an analytics-only project.

## Dataset Link

- **Dataset (Google Drive):** [food_ordering_behavior_dataset.csv](https://drive.google.com/file/d/1__bBUnmTq2-QQMZXj_QqQdSqjwgS8ABS/view?usp=drive_link) — 50,000 records, 19 columns (submitted alongside this report)

## GitHub & Project Demo Links

| Resource | Link |
|---|---|
| GitHub Repository | [radha-krishna-reddy/FoodOrdering-Consumertrends](https://github.com/radha-krishna-reddy/FoodOrdering-Consumertrends) |
| Tableau Public Dashboard | [View Dashboard](https://public.tableau.com/app/profile/radha.reddy/viz/FoodorderingbehaviourCustomertrendsAstructuredanalysisofchoicesandhabitsdashboard4/Dashboard2) |
| Project Demo Video | [Watch Demo](https://drive.google.com/file/d/1EqPvFY6cHxMu1EcVfxcAUui8lm5V3DC5/view?usp=sharing) |

## Documentation

Detailed supporting documents (all dated for the current design phase):

| Document | Contents |
|---|---|
| `Solution_Requirements.docx` | Full functional (FR-1–FR-6) and non-functional (NFR-1–NFR-6) requirements |
| `Technology_Stack.docx` | Architecture diagram, Table-1 (components), Table-2 (characteristics) |
| `Data_Flow_Diagrams_and_User_Stories.docx` | Level 0/1 DFDs and the complete 12-story backlog with acceptance criteria |

---

*Individual Submission — Project Design Phase II*
