# Software Engineering Midterm Study Guide

## 1. Introduction to Software Engineering

### Core Concepts
*   **Evolution of Roles:** Coder (Translates clear solution to code) &rarr; Programmer (Solves problems) &rarr; Developer (Defines problems) &rarr; Engineer (Designs overall architecture).
*   **Software Engineering Definition:** Understanding the context &rarr; Picking the right solution &rarr; Developing the best solution (effective & efficient). Going from a vague idea to an intuitive, scalable solution.
*   **Differences from other Engineering:** Software is intangible/invisible, built to evolve, and continues evolving long after initial release.

### Challenges & Benefits
*   **Software Crisis (60s & 70s to today):** Systems are never completed, miss deadlines, exceed budgets, fail requirements, are difficult to use, and lose user trust.
*   **Current Challenges:** Need for trustworthy quality, quick turnaround, increased complexity, diversity of systems, and handling **CHANGE**.
*   **Benefits of SE:** Applies proven techniques, predicts cost/schedule accurately, and builds desirable traits (reliability, maintainability, usability).
*   **The Team Approach:** Emphasizes *generalizing specialists* (cross-functional skills). Anyone can complete any task, and constant collaboration is required.

---

## 2. Software Development Life Cycle (SDLC)

### SDLC Overview
*   **Definition:** A structured, step-by-step process/roadmap to design, build, test, and deploy software. Minimizes risks, maximizes quality, and meets requirements.
*   **Technical Debt:** A poor implementation that saves 1 hour now can cost 20+ hours later.

### 6 Phases of the SDLC
| Phase | Goal | Who is involved | Process & Deliverables |
| :--- | :--- | :--- | :--- |
| **1. Requirements Analysis** | Define functional & non-functional requirements. | Business Analysts, PMs, Architects, Scrum Masters | Stakeholder discussions, prototyping. **Deliverables:** Use cases, UX design, approved requirements. |
| **2. Design** | Define architecture and component design. | Lead Developers, Architects, UI/UX Designers | Design discussions, architecture references. **Deliverables:** Database ERD, APIs, application UI/UX, infra design. |
| **3. Development** | Write code based on approved designs. | Developers, Lead Developers | Review designs, write code. **Deliverables:** Completed software programs/code. |
| **4. Testing** | Verify software against requirements. | Testers, Users | Develop and execute test cases. "Developers build it, Testers break it." **Deliverables:** Approved test results. |
| **5. Deployment** | Move software to the production environment. | Developers, Testers, PMs, Users | Coordinate deployment plan/schedule. **Deliverables:** Software in production, ready for users. |
| **6. Maintenance** | Keep software alive (updates, patches, support). | Developers, Testers, PMs, Users | Fix bugs, add features based on feedback. **Deliverables:** Updated application. |

---

## 3. Requirement Phase & WRSPM Model

### Requirements vs. Specifications
*   **Golden Rule:** Spending time strategically up front reduces cost/time later (e.g., 10h upfront saves 300h later).
*   **User Requirements:** Exact specifications of **WHAT** the software should do. Written in plain language from the client's point of view (e.g., "User should be able to log in").
*   **System Specifications:** Developer notes on **HOW** to meet the requirement technically, breaking it into smaller conditions without choosing the final tech stack yet (e.g., "Lock account after 5 failed attempts").

### Functional vs. Non-Functional Requirements
| Type | Focus | Missing Consequence | Example |
| :--- | :--- | :--- | :--- |
| **Functional** | What the system **does** (actions). | Product **does not work**. | User can reset password via email. |
| **Non-Functional** | **Constraints** on behavior (quality). | Product works **poorly**. | Uptime must be 99.9%. |

*   *Non-Functional Categories:* **Product** (must-haves, e.g., loads in 2s), **Organizational** (policies, e.g., Agile, code review), **External** (laws, e.g., GDPR, WCAG).

### WRSPM Model
A reference model connecting requirements to the real world.
*   **W (World):** Assumptions about the real environment (e.g., electricity, internet availability).
*   **R (Requirements):** What the user wants (plain language).
*   **S (Specifications):** Technical conditions bridging requirements to the solution.
*   **P (Program):** The actual code implementing the specs.
*   **M (Machine):** The hardware the software runs on.

*   *Variables:*
    *   **eh (Environment Hidden):** Environment parts the system cannot see (e.g., the physical bank card in a user's wallet).
    *   **ev (Environment Visible):** Environment parts exposed to the system (e.g., card's magnetic strip data).
    *   **sv (System Visible):** System parts exposed to the environment (e.g., ATM screen/buttons).
    *   **sh (System Hidden):** Internal workings unseen by users (e.g., cash roller, server calls).

---

## 4. Software Architecture & Design Patterns

### Architecture Fundamentals
*   **Definition:** The highest level of design; breaking larger systems into smaller, focused components.
*   **Analogy:** Skyscraper foundation or city zoning. Bad architecture cannot be fixed with good programming.
*   **Spaghetti Code:** Without architecture, files randomly link, bugs are hard to trace, and changes break everything.

### Common Design Patterns
| Pattern | Core Idea | Best For | Real Examples |
| :--- | :--- | :--- | :--- |
| **Pipe and Filter** | Data flows through independent filters. Rule: *Same type in, same type out*. | ETL pipelines, Compilers, CI/CD | Unix Shell, Data Warehouses (Kafka) |
| **Client-Server** | Central hub (Server) stores data/processes; Clients request/display data. | Web services, mobile apps | Online Gaming, YouTube |
| **Master-Slave** | Master commands; Slaves execute tasks and report back. Slaves do not communicate with each other. | DB replication, distributed systems | Grab App (Server=Master, Drivers=Slaves) |
| **Layered** | Stacked layers communicating only with adjacent layers (no skipping). | Web apps, Enterprise systems | MVC, Shopee |

*   *MVC Example (Layered):* **Model** (Data/DB) <-> **Controller** (Handles logic) <-> **View** (UI). View never talks directly to Model.
*   **Subsystem vs. Module:** A *Subsystem* has standalone value and can be plugged elsewhere. A *Module* operates inside a subsystem and has no independent value.

---

## 5. Software Design, Modularity, Coupling, and Cohesion

### Design vs. Coding
*   **Design** answers *how* real-world technologies will bring the architecture to life (e.g., picking Linux + MySQL).
*   Design is an **activity** (working together to structure software) and a **product** (the design document). It is *not* writing full implementation code.

### Modularity
*   **Goal:** Break programs into separate modules to achieve **Low Coupling** and **High Cohesion**.
*   **5 Goals of Modularity:** Abstraction, Understandability, Decomposability/Composability, Continuity (small change = localized impact), and Protectability.
*   **Information Hiding vs. Data Encapsulation:**
    *   *Information Hiding:* Hides complexity inside a black box.
    *   *Data Encapsulation:* Hides the data itself, restricting access via controlled getters and setters to validate input.

### Coupling (Connection Strength - Weaker is Better)
| Level | Type | Description | Solution / Fix |
| :--- | :--- | :--- | :--- |
| **Tight** | **Content** | Module directly reads/modifies another's internals. | Use Getters/Setters. |
| **Tight** | **Common** | Multiple modules read/write shared global data. | Route writes through one controller. |
| **Tight** | **External** | Multiple modules directly call an external API. | Create an API Controller. |
| **Medium** | **Control** | Passing flags/switches to control another's logic. | Split into specific methods without flags. |
| **Medium** | **Data Structure** | Multiple modules directly call the same data structure. | Use a Data Controller class. |
| **Loose** | **Data** | Pass only the exact data needed (not the whole object). | Keep data passing minimal. |
| **Loose** | **Message** | Send a command; receiver decides how to act. | Use clean interfaces. |

*   *Note:* "No Coupling" is an anti-pattern (creates a "God Module").

### Cohesion (Focus of a Module - Stronger is Better)
| Level | Type | Description |
| :--- | :--- | :--- |
| **Weak** | **Coincidental** | Grouped by chance (e.g., `utils.js`). Impossible to debug. |
| **Weak** | **Temporal** | Grouped by execution time (e.g., `onAppOpen()`). |
| **Weak** | **Logical** | Grouped by category but forced into a common interface. |
| **Medium** | **Procedural** | Sequential steps for a task, but reaches into unrelated domains. |
| **Medium** | **Communicational** | Share the same data, but dump unrelated operations together. |
| **Medium** | **Sequential** | Output of one step is input of the next, all in one domain. |
| **Strong** | **Functional** | One task perfectly defined. Clean input &rarr; calc &rarr; clean output. |
| **Strong** | **Object** | All activities only read/modify the attributes of a single object. |

*   **The Ultimate Goal:** Strong Cohesion + Loose Coupling. However, pushing cohesion too far (micro-modules) can accidentally increase coupling. Balance is key.