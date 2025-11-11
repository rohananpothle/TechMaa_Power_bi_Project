## 🧩 Data Collection Methods

This section explains how workforce activity and performance data is collected from various operational systems to power the **KPI Analytics & Live Performance Dashboard**.

---

### 1. Employee Login / Logout Data

**Objective:** Track daily active working hours, presence, and idle time.

**Source Options:**
- Attendance management systems (biometric, RFID, or web-based)
- Remote monitoring tools (Hubstaff, Clockify, ActivTrak)
- VPN or System Access logs

**Collection Methods:**
| Method | Description |
|--------|--------------|
| **API Integration** | Fetch login/logout and idle time using REST APIs from time-tracking tools. |
| **Database Connection** | Connect directly to SQL/Cloud database where attendance logs are stored. |
| **CSV/Excel Export** | Schedule daily/weekly exports dropped into a shared folder (OneDrive/SharePoint). |

**Key Data Fields:**  
`Employee_ID`, `Login_Time`, `Logout_Time`, `Date`, `Active_Hours`, `Idle_Hours`

---

### 2. Task Management System Logs

**Objective:** Measure task completion rate, on-time delivery, and workload distribution.

**Source Options:**
- Jira, Asana, Trello, ClickUp, or internal task tracking system

**Collection Methods:**
| Method | Description |
|--------|--------------|
| **REST API / Webhook** | Pull task details (status, assignee, time spent, due date) through APIs. |
| **Database Access** | Connect to internal project tracker database and extract task tables. |
| **CSV Exports** | Automate daily task data exports for ETL ingestion. |

**Key Data Fields:**  
`Task_ID`, `Task_Name`, `Assigned_To`, `Status`, `Start_Date`, `End_Date`, `Completion_Date`, `Estimated_Hours`, `Actual_Hours`

---

### 3. Session / Meeting Attendance Logs

**Objective:** Analyze session participation, training engagement, and learning effectiveness.

**Source Options:**
- Zoom, Microsoft Teams, Google Meet attendance reports
- Internal Learning Management System (LMS)

**Collection Methods:**
| Method | Description |
|--------|--------------|
| **API Access** | Fetch participant details, duration, and timestamps via APIs. |
| **CSV/Excel Reports** | Export meeting attendance reports from the platform. |
| **Manual Upload (Fallback)** | Store training feedback/attendance sheets in Google Sheets or Excel. |

**Key Data Fields:**  
`Session_ID`, `Employee_ID`, `Session_Date`, `Duration`, `Attendance_Status`, `Participation_Score`

---

### 4. CRM / Sales Data for Revenue KPIs

**Objective:** Calculate revenue conversion metrics and ROI per resource.

**Source Options:**
- Salesforce, Zoho CRM, HubSpot CRM
- Finance / Billing Database
- Internal Project Billing Tool

**Collection Methods:**
| Method | Description |
|--------|--------------|
| **CRM API Integration** | Retrieve deal and revenue information through CRM APIs. |
| **Database Access (SQL)** | Extract revenue, billing, and cost data from finance tables. |
| **Scheduled CSV Export** | Periodic export of CRM reports to shared folder for ETL. |

**Key Data Fields:**  
`Project_ID`, `Employee_ID`, `Billable_Hours`, `Revenue_Amount`, `Conversion_Rate`, `Date`

---

### 5. Activity Logs from Remote Work Tools

**Objective:** Track app usage, focus time, and engagement levels of remote employees.

**Source Options:**
- Hubstaff, ActivTrak, RescueTime, TimeDoctor
- Internal screen or system activity trackers

**Collection Methods:**
| Method | Description |
|--------|--------------|
| **REST APIs** | Fetch user-level activity duration, idle minutes, and productivity scores. |
| **Agent-Based Log Uploads** | Logs automatically sent from client systems to a central server. |
| **File-Based ETL** | Export and process CSV logs (application usage, activity duration). |

**Key Data Fields:**  
`Employee_ID`, `Date`, `Active_Minutes`, `Idle_Minutes`, `Focus_Score`, `Apps_Used`, `Screen_Time`

---

### ⚙️ ETL Integration Flow

```plaintext
[Data Sources]
↓
(1) API Calls / Database Queries / Scheduled CSV Exports
↓
(2) ETL Pipeline (Python / Power BI Dataflows / Azure Data Factory)
↓
(3) Transform & Merge on Employee_ID + Date
↓
(4) Load into Central Database or Power BI Dataset
↓
(5) KPI Dashboard & Predictive Insights
