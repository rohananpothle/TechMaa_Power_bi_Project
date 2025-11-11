# 📥 Data Features Collection

Each KPI visual relies on specific data features.
Below are the essential features (columns) required from each data source and their purpose.

# 🧭 1. Productivity Data (Worklog Table)

Data Source: Employee activity tracker / Time logs

| Feature Name      | Description                                    | Example    |
| ----------------- | ---------------------------------------------- | ---------- |
| EmployeeID        | Unique identifier for employee/intern          | EMP101     |
| Date              | Activity date                                  | 2025-11-11 |
| LoginTime         | Time when employee logged in                   | 09:05 AM   |
| LogoutTime        | Time when employee logged out                  | 06:10 PM   |
| ActiveHours       | Total productive hours                         | 7.5        |
| IdleHours         | Time marked as inactive / idle                 | 1.2        |
| TotalHours        | Sum of Active + Idle                           | 8.7        |
| TasksAssigned     | Count of tasks assigned on that day            | 6          |
| TasksCompleted    | Count of tasks completed                       | 5          |
| ContributionScore | Derived productivity score (system-calculated) | 82         |
| Department        | Team/Department (Tech, Sales, Marketing)       | Sales      |

| **KPI Name**                      | **Required Features (Columns)**                         | **Source Table** | **Purpose / Usage in Power BI**                       |
| --------------------------------- | ------------------------------------------------------- | ---------------- | ----------------------------------------------------- |
| **Active Working Hours**          | `EmployeeID`, `Date`, `ActiveHours`, `Department`       | `Worklog`        | X-Axis → Date / Employee<br>Y-Axis → Sum(ActiveHours) |
| **Idle Time Ratio**               | `IdleHours`, `TotalHours`, `EmployeeID`, `Date`         | `Worklog`        | Calculate ratio `IdleHours / TotalHours`              |
| **Daily Work Contribution Score** | `ContributionScore`, `Date`, `EmployeeID`               | `Worklog`        | Plot avg(ContributionScore) by Date or Department     |
| **Task Completion %**             | `TasksCompleted`, `TasksAssigned`, `EmployeeID`, `Date` | `Worklog`        | DAX = TasksCompleted / TasksAssigned                  |
| **Task Efficiency**               | `TasksCompleted`, `TasksAssigned`, `Department`         | `Worklog`        | Compare efficiency across employees or teams          |

        Task Completion % = DIVIDE(SUM('Worklog'[TasksCompleted]), SUM('Worklog'[TasksAssigned]), 0) * 100
        Idle Time Ratio = DIVIDE(SUM('Worklog'[IdleHours]), SUM('Worklog'[TotalHours]), 0)

# 🧩 Used For:
1. Active Working Hours
2. Idle Time Ratio
3. Daily Work Contribution Score
4. Task Efficiency (Tasks Completed / Tasks Assigned)

# 🕒 2. Attendance & Participation Data (Attendance Table)

Data Source: Session logs / Meeting platform API

| Feature Name       | Description                                | Example    |
| ------------------ | ------------------------------------------ | ---------- |
| EmployeeID         | Unique identifier                          | EMP101     |
| Date               | Session date                               | 2025-11-11 |
| TotalSessions      | Number of sessions scheduled               | 3          |
| SessionsAttended   | Sessions attended by employee              | 2          |
| AttendanceRate     | Derived = SessionsAttended / TotalSessions | 66%        |
| EngagementDuration | Time spent in sessions                     | 95 mins    |
| InteractionCount   | Questions, chats, or polls participated    | 4          |
| EngagementPoints   | Weighted engagement metric                 | 72         |
| L&DPoints          | Learning module points (from LMS)          | 85         |

| **KPI Name**                                   | **Required Features (Columns)**                                            | **Source Table** | **Purpose / Usage in Power BI**                       |
| ---------------------------------------------- | -------------------------------------------------------------------------- | ---------------- | ----------------------------------------------------- |
| **Daily Session Attendance Rate**              | `SessionsAttended`, `TotalSessions`, `EmployeeID`, `Date`                  | `Attendance`     | DAX = SessionsAttended / TotalSessions                |
| **Engagement in Live Sessions**                | `EngagementDuration`, `InteractionCount`, `EngagementPoints`, `Department` | `Attendance`     | Analyze engagement over time or across departments    |
| **Learning & Development Participation Score** | `L&DPoints`, `EmployeeID`, `Department`, `Date`                            | `Attendance`     | Evaluate training participation per intern/department |

    Attendance Rate = DIVIDE(SUM('Attendance'[SessionsAttended]), SUM('Attendance'[TotalSessions]), 0) * 100
    Engagement Score = AVERAGE('Attendance'[EngagementPoints])
    L&D Score = AVERAGE('Attendance'[L&DPoints])

# 🧩 Used For:
1. Daily Session Attendance Rate
2. Engagement in Live Sessions
3. Learning & Development Participation Score

# 🧮 3. Performance Evaluation Data (Evaluation Table)

Data Source: Task QA feedback, mentor reviews, system evaluations

| Feature Name    | Description                 | Example              |
| --------------- | --------------------------- | -------------------- |
| EmployeeID      | Unique identifier           | EMP101               |
| TaskID          | Task identifier             | TSK202               |
| EvaluationDate  | Review date                 | 2025-11-11           |
| SubmittedOnTime | Boolean (1=Yes, 0=No)       | 1                    |
| QualityScore    | Reviewer score (out of 100) | 88                   |
| ReviewComments  | Qualitative feedback        | “Excellent accuracy” |

| **KPI Name**               | **Required Features (Columns)**                                         | **Source Table**                                | **Purpose / Usage in Power BI**                       |
| -------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------- | ----------------------------------------------------- |
| **Timely Submission Rate** | `SubmittedOnTime`, `TaskID`, `EmployeeID`, `EvaluationDate`             | `Evaluation`                                    | DAX = (Count SubmittedOnTime = 1) / Total Evaluations |
| **Quality Score**          | `QualityScore`, `EvaluationDate`, `Department`, `EmployeeID`            | `Evaluation`                                    | Avg QualityScore by Employee / Team                   |
| **Performance Index**      | Weighted avg of (`Task Efficiency`, `Attendance Rate`, `Quality Score`) | Combined from Worklog + Attendance + Evaluation | Calculate using DAX weighted model                    |

        Timely Submission Rate = 
        DIVIDE(
            COUNTROWS(FILTER('Evaluation', 'Evaluation'[SubmittedOnTime] = 1)),
            COUNTROWS('Evaluation'),
            0
        ) * 100
        
        Performance Index = 
        0.4 * [Task Efficiency] + 
        0.3 * [Attendance Rate] + 
        0.3 * [Quality Score]


# 🧩 Used For:
1. Timely Submission Rate
2. Quality Score
3. Performance Index

# 💰 4. CRM / Revenue Data (CRM Table)

Data Source: CRM system (HubSpot, Zoho, or manual leads tracker)

| Feature Name     | Description                           | Example       |
| ---------------- | ------------------------------------- | ------------- |
| InternID         | Unique identifier                     | INT203        |
| LeadID           | Lead unique ID                        | L1001         |
| LeadSource       | Channel (LinkedIn, Referral, WebForm) | LinkedIn      |
| LeadStatus       | Current stage (Open, Won, Lost)       | Closed Won    |
| LeadDate         | Date of lead creation                 | 2025-11-10    |
| RevenueGenerated | Sale value from lead                  | ₹12,500       |
| ProductCategory  | Product/service sold                  | Cloud Hosting |
| ConversionDate   | Date converted to sale                | 2025-11-12    |

| **KPI Name**                           | **Required Features (Columns)**                              | **Source Table** | **Purpose / Usage in Power BI**        |
| -------------------------------------- | ------------------------------------------------------------ | ---------------- | -------------------------------------- |
| **Leads Generated by Interns**         | `InternID`, `LeadID`, `LeadDate`, `Department`               | `CRM`            | Count of leads per intern or per month |
| **Lead-to-Sale Conversion Ratio**      | `LeadStatus` (Open, Won, Lost), `LeadDate`, `ConversionDate` | `CRM`            | DAX = ConvertedLeads / TotalLeads      |
| **Revenue Impact Score**               | `RevenueGenerated`, `InternID`, `ProductCategory`            | `CRM`            | Compare revenue by intern or category  |
| **Monthly Revenue Contribution Trend** | `RevenueGenerated`, `LeadDate`, `ConversionDate`             | `CRM`            | Line chart for monthly trends          |

        Total Leads = COUNTROWS('CRM')
        Converted Leads = COUNTROWS(FILTER('CRM', 'CRM'[LeadStatus] = "Closed Won"))
        Conversion Rate = DIVIDE([Converted Leads], [Total Leads], 0) * 100
        Total Revenue = SUM('CRM'[RevenueGenerated])


# 🧩 Used For:
1. Leads Generated
2. Lead-to-Sale Conversion Ratio
3. Revenue Impact Score
4. Monthly Revenue Contribution Trend

# 🧾 5. Master Data (Employee Table)

Data Source: HR/Internship Management System

| Feature Name | Description                          | Example        |
| ------------ | ------------------------------------ | -------------- |
| EmployeeID   | Unique identifier                    | EMP101         |
| FullName     | Employee name                        | Rohan Anpothle |
| Role         | Job title (Intern, Analyst, Manager) | Intern         |
| Department   | Department name                      | Data Analytics |
| JoinDate     | Date of joining                      | 2025-07-01     |
| Supervisor   | Reporting manager                    | Asghar         |
| Status       | Active/Inactive                      | Active         |

| **Feature**  | **Purpose**                                        | **Used Between Tables**                        |
| ------------ | -------------------------------------------------- | ---------------------------------------------- |
| `EmployeeID` | Primary Key for joins                              | `Employee ↔ Worklog ↔ Attendance ↔ Evaluation` |
| `InternID`   | Key for sales interns                              | `Employee ↔ CRM`                               |
| `Date`       | Time intelligence, trend charts                    | All tables (through Date Table)                |
| `Department` | Filter for dashboards                              | All tables                                     |
| `Role`       | Slicer for segmentation (Intern, Analyst, Manager) | `Employee`                                     |


# 🧩 Used For:
1. Relating all tables (Primary Key)
2. Segmentation filters in Power BI slicers

# 🗂️ Summary Table (For Power BI Model)

| KPI Category | Primary Table       | Key Columns Required                                                           | Example Visual Type               |
| ------------ | ------------------- | ------------------------------------------------------------------------------ | --------------------------------- |
| Productivity | `Worklog`           | EmployeeID, Date, ActiveHours, IdleHours, TasksCompleted, TasksAssigned        | Line Chart / Column Chart / Gauge |
| Attendance   | `Attendance`        | EmployeeID, Date, SessionsAttended, TotalSessions, EngagementPoints, L&DPoints | Line / Donut / Stacked Bar        |
| Performance  | `Evaluation`        | EmployeeID, QualityScore, SubmittedOnTime, EvaluationDate                      | Bar / Line / Table                |
| Revenue      | `CRM`               | InternID, LeadID, LeadStatus, RevenueGenerated, ConversionDate                 | Funnel / TreeMap / Line           |
| Filters      | `Employee` + `Date` | Department, Role, JoinDate                                                     | Global slicers                    |


# 🧠 Data Integration Notes
1. All tables will be connected via EmployeeID or InternID.
2. Use Power Query to:
    1. Merge Attendance + Worklog + Tasks + Evaluation tables.
    2. Clean timestamps, handle nulls, and normalize data types.
3. Set Date Table as a Calendar Table in Power BI for time intelligence.
4. Build relationships:
   
        Employee[EmployeeID] 1—* Worklog[EmployeeID]
        Employee[EmployeeID] 1—* Attendance[EmployeeID]
        Employee[EmployeeID] 1—* Evaluation[EmployeeID]
        Employee[EmployeeID] 1—* CRM[InternID]
