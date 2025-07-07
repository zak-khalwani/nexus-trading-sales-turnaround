# Nexus Trading Co. Sales Turnaround: A Power BI Case Study

<p align="center">
  <a href="https://tinyurl.com/ywmuyhsc" target="_blank">
    <img src="https://img.shields.io/badge/Live_Dashboard-View_Here-brightgreen?style=for-the-badge&logo=powerbi" alt="Live Dashboard Link">
  </a>
</p>

This repository documents a Power BI sales analytics solution designed for "Nexus Trading Co.," a fictional international distributor. It showcases how a well-designed dashboard can transform raw transactional data into a strategic command center, enabling leadership to move from reactive decision-making to proactive, data-driven strategy.

![Dashboard Demo](assets/dashboard_demo.gif)

## Table of Contents
- [1. Case Study Overview](#1-case-study-overview)
  - [The Business Problem](#the-business-problem)
  - [The Solution: A Centralized Analytics Hub](#the-solution-a-centralized-analytics-hub)
  - [Key Outcomes](#key-outcomes)
  - [Tech Stack](#tech-stack)
- [2. Technical Deep Dive](#2-technical-deep-dive)
  - [Data Modeling: The Star Schema](#data-modeling-the-star-schema)
  - [Analytical Power: DAX Measures](#analytical-power-dax-measures)
- [3. Repository Structure](#3-repository-structure)
- [4. How to Explore This Project](#4-how-to-explore-this-project)

---

## 1. Case Study Overview

### The Business Problem
"Nexus Trading Co." was facing a common but critical challenge: despite having access to vast amounts of sales data, the company lacked clarity. The leadership team was flying blind, unable to answer fundamental questions with confidence:
*   Are we growing profitably, or just chasing revenue?
*   Which of our sales channels—Wholesale, Distributor, or Export—is the most effective?
*   Which products and stores are our true profit drivers, and which are lagging?
*   How is our performance trending compared to last year?

Decisions were being made in silos, based on gut feelings and incomplete static reports, leading to missed opportunities and unidentified performance gaps.

### The Solution: A Centralized Analytics Hub
The objective was to design and deploy a dynamic, interactive Power BI dashboard to serve as the single source of truth for sales performance. This tool was built to democratize data, allowing managers and executives to explore insights, identify trends, and make strategic decisions in real-time. The focus was on creating a holistic view that connected sales with profitability.

### Key Outcomes
The dashboard directly addressed the business problems by enabling:
*   **Instant YoY Performance Tracking:** All key metrics include year-over-year growth percentages, providing immediate context.
*   **Profitability Analysis:** By incorporating `Profit Margin` alongside `Total Sales`, the business can now identify high-revenue, low-profit areas that require strategic intervention.
*   **Clear Performance Segmentation:** The dashboard clearly breaks down performance by sales channel, store location, top products, and top customers.
*   **Empowered Leadership:** Provided a tool for the management team to conduct their own analysis, fostering a culture of data-driven inquiry.

### Tech Stack
*   **Data Analysis & Visualization:** Power BI Desktop & Power BI Service
*   **Data Modeling & Calculations:** DAX
*   **Data Transformation & Cleaning (ETL):** Power Query

---

## 2. Technical Deep Dive

The dashboard's intuitive front-end is powered by a robust and optimized back-end.

### Data Modeling: The Star Schema
The data model utilizes a best-practice **Star Schema**. This design, featuring a central `Sales` fact table connected to `Dates`, `Products`, `Regions`, and `Customers` dimension tables, is the gold standard for analytics. It ensures fast performance, scalability, and ease of use when creating complex measures.

![Data Model](assets/data%20model.png)

### Analytical Power: DAX Measures
The core business logic is encapsulated in DAX (Data Analysis Expressions). Key measures like `Total Sales`, `Profit Margin`, and Year-over-Year calculations (`% Sales Growth`) were created to provide the rich insights seen on the dashboard.

**For a complete breakdown of the data model and all key DAX measures, please see the `docs/` folder.**

---

## 3. Repository Structure
The repository is organized for clarity and ease of use.

<pre>
.
├── assets/
│ ├── dashboard_demo.gif
│ ├── dashboard_overview.png
│ └── data_model.png
├── docs/
│ ├── 01_Business_Context.md
│ ├── 02_Data_Model_and_Sources.md
│ └── 03_DAX_Measures.md
├── .gitignore
└── README.md
</pre>

---

## 4. How to Explore This Project
1.  **Interact with the Live Dashboard:**
    *   Click the "Live Dashboard" badge at the top of this page or go directly to: [https://tinyurl.com/ywmuyhsc](https://tinyurl.com/ywmuyhsc)
2.  **Review the Documentation:**
    *   For a deeper understanding of the business logic and technical implementation, review the detailed markdown files in the `docs/` folder.
