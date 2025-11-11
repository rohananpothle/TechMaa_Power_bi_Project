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

# 🧩 Used For:
1. Relating all tables (Primary Key)
2. Segmentation filters in Power BI slicers

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
