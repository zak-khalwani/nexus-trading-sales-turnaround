# 2. Data Model and Sources

This document describes the underlying data architecture of the Nexus Trading Co. dashboard.

## Data Sources

The data for this case study was modeled to represent typical transactional systems found in a distribution company. In a real-world scenario, the data would be sourced from:

*   **ERP System / SQL Database:** For the core `Sales` transaction table.
*   **CRM System:** For the `Customers` dimension table.
*   **Product Information Management (PIM) System:** For the `Products` dimension table.

For this project, all data was combined and transformed using Power Query Editor within Power BI Desktop to ensure data quality and model efficiency.

## Data Model: The Star Schema

The project is built on a **Star Schema**, the industry best-practice for analytical data modeling. This structure provides optimal query performance, simplicity, and scalability. It features a central fact table (`Sales`) linked to several descriptive dimension tables.

![Data Model Diagram](../assets/data%20model.png)
*(Note: The `../` in the path allows the image in the parent `assets` folder to be viewed from the `docs` folder on GitHub)*

### Table Descriptions

| Table       | Type      | Description                                                                                             |
|-------------|-----------|---------------------------------------------------------------------------------------------------------|
| **Sales**   | Fact      | The heart of the model. Contains all individual sales transaction records. Each row is a unique order line. |
| **Dates**   | Dimension | A standard calendar table providing time-based attributes (Year, Quarter, Month) for trend analysis.      |
| **Products**| Dimension | A unique list of all products sold by Nexus Trading Co., including their names and groupings.           |
| **Regions** | Dimension | Contains geographic information about the company's physical store locations (city and country).        |
| **Customers** | Dimension | A unique list of all customers, allowing for analysis of customer-specific profitability and value.     |

### Relationships

*   All dimension tables (`Dates`, `Products`, `Regions`, `Customers`) have a **one-to-many relationship** (`1-to-*`) filtering the `Sales` fact table. This clean, unidirectional filtering path is key to the model's performance and accuracy.

