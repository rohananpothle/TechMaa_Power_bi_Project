# 🧠 TechMaa KPI Analytics & Live Performance Dashboard  
## 📋 Meeting Questionnaire  

This document outlines the key discussion points and questions to be asked to **TechMaa data source teams, internal project members (interns), and management** during the requirement and planning phase of the project.  

---

## 🔹 Section 1: Data Source / IT Team Discussion

| **Category** | **Questions** | **Response / Notes** |
|---------------|----------------|----------------------|
| **Data Availability** | What are the main sources of employee activity data? (MSIS, Excel logs, CRM, Attendance DB, etc.) |  |
|  | How frequently is data updated (real-time, daily, weekly)? |  |
|  | Who owns or manages these data sources? |  |
|  | Where is data stored (SQL Server, Firebase, Google Drive, internal API)? |  |
|  | Are there any access restrictions for analytics use? |  |
| **Data Structure & Quality** | What fields are present in the raw logs (Employee ID, Task ID, Start Time, End Time, Status, etc.)? |  |
|  | Is Employee ID consistent across all systems? |  |
|  | Are timestamps stored in local time or UTC? |  |
|  | Are there frequent missing or duplicate values? |  |
| **Data Extraction** | What file formats are used (Excel, CSV, JSON, SQL Table)? |  |
|  | Can we schedule automatic exports or API calls? |  |
|  | How often should ETL be refreshed? |  |
| **Security & Privacy** | Are there any confidentiality rules for employee data? |  |
|  | Should dashboards anonymize names for interns/employees? |  |
|  | Who can view the final dashboard (Management, HR, Leads)? |  |

---

## 🔹 Section 2: Internal Project Team (Interns & Analysts)

| **Category** | **Questions** | **Response / Notes** |
|---------------|----------------|----------------------|
| **Project Understanding** | What is the main objective of the dashboard (Productivity tracking, Engagement, ROI)? |  |
|  | Who are the primary stakeholders or end users? |  |
| **KPI Definition** | How do we define productive vs. idle hours? |  |
|  | How should task completion rate be calculated? |  |
|  | Should we include YTD, MTD, or QTD metrics? |  |
|  | How will we calculate performance index (weighted KPI model)? |  |
| **Data Cleaning** | Who is responsible for handling missing or inconsistent data? |  |
|  | Which tools will be used for transformation (Python, Power Query, Excel)? |  |
|  | What is the process for data validation before loading into Power BI? |  |
| **Dashboard Design** | What visuals are required (KPI Cards, Gauge, Heatmap, Line Trend, Bar Chart)? |  |
|  | What filters/slicers should we include (Date, Department, Role)? |  |
|  | Should we have drill-through pages for employee-level data? |  |
|  | What theme or branding matches TechMaa’s identity? |  |
| **Roles & Responsibilities** | Who will handle Data Cleaning & Transformation? |  |
|  | Who will develop DAX formulas and measures? |  |
|  | Who will design visuals and publish the dashboard? |  |
|  | Who will perform testing and prepare documentation? |  |
| **Reporting & Delivery** | How often should the Power BI dashboard refresh? |  |
|  | What output formats are expected (Dashboard, PDF, Excel Reports)? |  |
|  | What is the final presentation date and review schedule? |  |

---

## 🔹 Section 3: HR / Management Stakeholder Discussion

| **Category** | **Questions** | **Response / Notes** |
|---------------|----------------|----------------------|
| **Key Metrics & KPIs** | What are the most important KPIs you want monitored? (Utilization %, Task Completion %, Productivity Index, etc.) |  |
|  | Should we display data at individual or departmental level? |  |
|  | Do you want alerts or predictive insights (e.g., low performance alerts)? |  |
| **Report Format** | Do you prefer summarized dashboards or detailed reports? |  |
|  | How frequently should reports be shared (daily, weekly, monthly)? |  |
|  | Should we include trend forecasting or historical comparisons? |  |
| **Access Control** | Who will access the dashboard? (HR, Department Heads, CEO) |  |
|  | Do you want separate dashboards for interns vs. employees? |  |
|  | Should we restrict financial KPIs to management only? |  |
| **Future Scope** | Are you open to integrating predictive models for performance forecasting? |  |
|  | Should this system eventually connect with HRMS or Payroll systems? |  |

---

## 🔹 Section 4: Automation / Technical Integration

| **Category** | **Questions** | **Response / Notes** |
|---------------|----------------|----------------------|
| **ETL Scheduling** | Should data refresh automatically (Power BI Gateway / Cron Job)? |  |
|  | What is the frequency for updates (hourly/daily)? |  |
| **Integration** | Are APIs available for direct connection to attendance or CRM systems? |  |
|  | Should Python scripts automate preprocessing? |  |
| **Reporting Automation** | Do you need automated daily/weekly summary emails? |  |
|  | Should performance scorecards be exported to PDF/Excel automatically? |  |

---

## 🧩 Section 5: Meeting Action Items

| **Action Point** | **Owner** | **Deadline** | **Remarks** |
|-------------------|------------|---------------|--------------|
| Data source confirmation | Data Source Team | 15 Nov 2025 |  |
| KPI definitions finalized | Analytics Team | 16 Nov 2025 |  |
| Power BI dashboard design approved | Project Lead | 17 Nov 2025 |  |
| Automation & refresh setup | Tech Team | 17 Nov 2025 |  |
| Final review with management | All Stakeholders | 17 Nov 2025 |  |

---

## 🧾 Notes
- All interns should update progress in the shared tracker daily.  
- Weekly review calls with the Data Source Team to ensure data accuracy.  
- All datasets must be stored in a central secured location (e.g., OneDrive or SQL).  
