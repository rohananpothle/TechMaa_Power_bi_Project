# Features list:

  1. EmployeeID
  2. Date
  3. LoginTime
  4. LogoutTime
  5. ActiveHours
  6. IdleHours
  7. TotalHours
  8. TasksAssigned
  9. TasksCompleted
  10. ContributionScore
  11. Department
  12. DataSource

productivity-kpi-dashboard/
│
├── README.md
├── dataset_description.md
├── calculated_columns.md
├── kpi_definitions.md
├── dax_measures.md
├── powerbi_workflow.md
├── visuals_guide.md
└── images/

# Productivity KPI Dashboard (Power BI)

This project analyzes employee productivity, performance, attendance, and task efficiency using time logs and task-level data.

The dataset includes:
- Employee Working Hours (Active, Idle, Total)
- Login/Logout Times
- Tasks Assigned & Completed
- Contribution Score
- Date & Department information

The dashboard provides insights into:
- Productivity KPIs
- Task Performance KPIs
- Attendance Metrics
- Contribution & Efficiency Trends
- Department-Level Performance

---

## 📁 Repository Contents

| File | Description |
|------|-------------|
| `dataset_description.md` | Columns & data types overview |
| `calculated_columns.md` | List of all calculated columns derived from dataset |
| `kpi_definitions.md` | 27+ KPIs with formulas & explanations |
| `dax_measures.md` | Ready-to-use DAX measures for Power BI |
| `powerbi_workflow.md` | Step-by-step workflow from data cleaning to dashboard |
| `visuals_guide.md` | Recommended visuals for each KPI category |

---

## 🚀 Tools Used
- **Power BI Desktop**
- **DAX Calculations**
- **Power Query (M Language)**

---

## 📊 Final Deliverables
- Productivity Dashboard
- Task Performance Dashboard
- Attendance & Availability Report
- Contribution & Efficiency Trends
- Department-Level Insights

---

## 🤝 Contribute
Feel free to raise issues or submit PRs to improve the KPIs or add more visuals.

---

# Dataset Description

Below are the fields available in the dataset after initial processing:

| Column Name        | Description |
|--------------------|-------------|
| EmployeeID         | Unique employee ID |
| Date               | Activity date |
| LoginTime          | Login timestamp |
| LogoutTime         | Logout timestamp |
| ActiveHours        | Number of hours employee was actively working |
| IdleHours          | Hours employee was idle |
| TotalHours         | Total hours logged |
| TasksAssigned      | Number of tasks assigned |
| TasksCompleted     | Number of tasks completed |
| ContributionScore  | Daily contribution score |
| Department         | Employee department |
| DataSource         | Source of the record |

All columns were transformed into proper data types using Power Query.

# Calculated Columns (Derived from Dataset)

These columns are created using DAX or Power Query.

## 🧭 Productivity Calculated Columns

1. ActiveTimePerc = DIVIDE([ActiveHours], [TotalHours])
2. IdleTimePerc = DIVIDE([IdleHours], [TotalHours])
3. ProductivityRatio = DIVIDE([ActiveHours], [ActiveHours] + [IdleHours])
4. LoginDurationHours = DATEDIFF([LoginTime], [LogoutTime], MINUTE) / 60
5. TaskCompletionPerc = DIVIDE([TasksCompleted], [TasksAssigned])
6. TaskEfficiency = DIVIDE([TasksCompleted], [TasksAssigned])
7. TaskBacklog = [TasksAssigned] - [TasksCompleted]
8. HoursPerTask = DIVIDE([ActiveHours], [TasksCompleted])
---

## 🕒 Attendance Calculated Columns

9. IsPresent = IF([TotalHours] > 0, 1, 0)
10. DailyWorkingHours = [TotalHours]


---

## 📈 Trend Columns

11. **Year**
12. **Month**
13. **Week Number**
14. **Quarter**

Derived using Date column.


# KPI Definitions

This file includes the essential KPIs calculated in the dashboard.

---

## 🧭 Productivity KPIs

### 1. Active Working Hours
`SUM(ActiveHours)`

### 2. Idle Time Ratio
`IdleHours / TotalHours`

### 3. Productivity Percentage
`ActiveHours / TotalHours`

### 4. Daily Contribution Score
`SUM(ContributionScore)`

---

## 🧮 Task Performance KPIs

### 5. Tasks Assigned
`SUM(TasksAssigned)`

### 6. Tasks Completed
`SUM(TasksCompleted)`

### 7. Task Completion Percentage
`TasksCompleted / TasksAssigned`

### 8. Task Efficiency
Same: `TasksCompleted / TasksAssigned`

### 9. Task Backlog
`TasksAssigned - TasksCompleted`

### 10. Average Time per Task
`ActiveHours / TasksCompleted`

---

## 🕒 Attendance KPIs

### 11. Present Days
Flag where TotalHours > 0

### 12. Attendance Rate
`PresentDays / TotalDays`

### 13. Average Login Duration
`AVG(LoginDurationHours)`

### 14. Daily Working Hours
`SUM(TotalHours)`

---

## 🧮 Performance KPIs

### 15. Performance Index (Weighted)
    Example:
    
    PerformanceIndex =
    0.4 * [TaskCompletionPerc] +
    0.3 * [EngagementScore]

    or
    PerformanceIndex =
    0.4 * [TaskEfficiency] +
    0.3 * [Productivity Percentage]
    


### 16. Output Per Hour
`TasksCompleted / ActiveHours`

### 17. Quality Score
`TaskCompletionPerc × Productivity %`

---

## 🏢 Department KPIs

### 18. Department Productivity
`SUM(ActiveHours) by Dept`

### 19. Department Efficiency
`AVG(TaskCompletionPerc)`

### 20. Department Load
`SUM(TasksAssigned)`

# DAX Measures for Power BI

Below are ready-to-use DAX measures:

---

## Productivity Measures

  1. Total Active Hours: Total Active Hours = SUM('Data'[ActiveHours])
  2. Total Idle Hours: Total Idle Hours = SUM('Data'[IdleHours])
  3. Active Time %: Active Time % = DIVIDE([Total Active Hours], [Total Hours])
  4. Idle Time %: Idle Time % = DIVIDE([Total Idle Hours], [Total Hours])

---

## Task Measures

  1. Tasks Assigned: Tasks Assigned = SUM('Data'[TasksAssigned])
  2. Tasks Completed: Tasks Completed = SUM('Data'[TasksCompleted])
  3. Task Completion %: Task Completion % = DIVIDE([Tasks Completed], [Tasks Assigned])
  4. Tasks Backlog: Task Backlog = [Tasks Assigned] - [Tasks Completed]

---

## Attendance Measures

  1. Present Days: Present Days = CALCULATE(COUNTROWS('Data'), 'Data'[TotalHours] > 0)
  2. Tasks Completed: Tasks Completed = SUM('Data'[TasksCompleted])
  3. Task Completion %: Task Completion % = DIVIDE([Tasks Completed], [Tasks Assigned])
  4. Tasks Backlog: Task Backlog = [Tasks Assigned] - [Tasks Completed]

---

## Attendance Measures

  1. Present Days: Present Days = CALCULATE(COUNTROWS('Data'), 'Data'[TotalHours] > 0)
  2. Attendance %: Attendance % = DIVIDE([Present Days], DISTINCTCOUNT('Data'[Date]))

---

## Performance Measures

  1. Performance Index:
              Performance Index =
              0.4 * [Task Completion %] +
              0.3 * [Active Time %] +
              0.3 * [Output per Hour]
  2. Output per Hour: Output per Hour = DIVIDE([Tasks Completed], [Total Active Hours])


# Power BI Workflow

## 1. Import Data
Use Power Query to clean and assign data types.

## 2. Create Calculated Columns
Define productivity, attendance, and task columns.

## 3. Create Measures
Use DAX to generate KPI measures.

## 4. Build Visuals
Generate trend, productivity, and performance dashboards.

## 5. Add Filters, Slicers, Drilldowns
- Employee
- Department
- Date (Year/Month/Week)

## 6. Publish to Power BI Service
- Create daily/weekly refresh schedule

## 7. Share the dashboard with stakeholders



# Visuals Guide for Productivity Dashboard

| KPI Category | Recommended Visual |
|--------------|--------------------|
| Productivity KPIs | KPI Card, Gauge, Donut Chart |
| Task KPIs | Clustered Bar, Line Chart, Table |
| Attendance KPIs | Area Chart, Column Chart |
| Performance KPIs | Radar Chart, Line Chart |
| Department KPIs | Treemap, Matrix |
| Trends | Line Chart, Ribbon Chart |

---

## Dashboard Layout (Recommended)
1. **Header Section**  
   - Overall Productivity  
   - Task Completion  
   - Contribution Score  

2. **Productivity Analysis**  
   - Active vs Idle Time  
   - Trend by date  

3. **Task Performance Section**  
   - Tasks Assigned vs Completed  
   - Efficiency & Backlog  

4. **Attendance Analytics**  
   - Present Days  
   - Average Working Hours  

5. **Department Insights**  
   - Productivity by Dept  
   - Task Load by Dept  
















