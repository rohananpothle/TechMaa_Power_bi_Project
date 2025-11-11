# 📊 TechMaa KPI Analytics Power BI Dashboard Design

## 🧭 Dashboard Pages Overview
| Page | Focus Area | Key Visuals | Primary Tables Used |
|-------|-------------|--------------|----------------------|
| **1️⃣ Overview** | All KPIs snapshot | KPI cards, Gauge charts, Summary trend | All tables |
| **2️⃣ Productivity Dashboard** | Work efficiency | Active hours, Task completion, Idle ratio | Worklog |
| **3️⃣ Attendance & Participation** | Engagement & training | Attendance rate, Engagement trend | Attendance |
| **4️⃣ Performance Evaluation** | Quality & timeliness | Performance index, Quality score | Evaluation |
| **5️⃣ Revenue Analytics** | Intern revenue & sales | Leads, Conversion, Revenue trend | CRM |
| **6️⃣ Employee Summary** | Filters & drillthrough | Employee-wise metrics | Employee |

---

## 🧩 1. Overview Dashboard (Executive Summary)
| Visual Type | X-Axis / Category | Y-Axis / Value | Filters / Slicers | Purpose |
|--------------|-------------------|----------------|--------------------|----------|
| **KPI Cards** | — | Total Employees, Avg Active Hours, Task Completion %, Attendance Rate, Conversion Rate | Date, Department | Show overall status of organization |
| **Line Chart** | Date | Performance Index | Department | Performance trend over time |
| **Clustered Column Chart** | Department | Avg Active Hours, Task Efficiency % | Date | Compare productivity between departments |
| **Gauge Chart** | — | Overall Productivity Score | — | Show progress vs target (e.g., 80%) |
| **Donut Chart** | Department | Employee Count | Status (Active/Inactive) | Workforce distribution |

**📘 DAX Tips:**
```DAX
Task Efficiency % = DIVIDE(SUM('Worklog'[TasksCompleted]), SUM('Worklog'[TasksAssigned]), 0) * 100
Performance Index = 0.4*[Task Efficiency %] + 0.3*[Attendance Rate] + 0.3*[Quality Score]
```

---

## 🧭 2. Productivity Dashboard
| Visual Type | X-Axis | Y-Axis / Value | Filters / Slicers | Table | Purpose |
|--------------|--------|----------------|--------------------|--------|----------|
| **Line Chart** | Date | ActiveHours | EmployeeID, Department | Worklog | Show working hour trend |
| **Column Chart** | EmployeeID | TaskEfficiency | Department, Date | Worklog | Compare task performance |
| **Stacked Column Chart** | Date | ActiveHours, IdleHours | Department | Worklog | Display productivity vs idle ratio |
| **Gauge Chart** | — | Avg ContributionScore | — | Worklog | Overall contribution index |
| **Heatmap (Matrix)** | Date | EmployeeID | ActiveHours | Department | Identify low-activity days |

**📘 DAX:**
```DAX
Idle Time Ratio = DIVIDE(SUM('Worklog'[IdleHours]), SUM('Worklog'[TotalHours]), 0)
Daily Contribution Score = AVERAGE('Worklog'[ContributionScore])
```

---

## 🕒 3. Attendance & Participation Dashboard
| Visual Type | X-Axis | Y-Axis / Value | Filters / Slicers | Table | Purpose |
|--------------|--------|----------------|--------------------|--------|----------|
| **Line Chart** | Date | AttendanceRate | Department | Attendance | Show attendance trend |
| **Stacked Bar Chart** | EmployeeID | SessionsAttended | Department, Date | Attendance | Compare session attendance |
| **Donut Chart** | Department | Avg AttendanceRate | — | Attendance | Show department engagement |
| **Column Chart** | Date | EngagementPoints, L&DPoints | EmployeeID | Attendance | Track engagement vs learning |
| **Card Visuals** | — | Avg EngagementPoints, L&D Score | Department | Attendance | Show participation highlights |

**📘 DAX:**
```DAX
Attendance Rate = DIVIDE(SUM('Attendance'[SessionsAttended]), SUM('Attendance'[TotalSessions]), 0) * 100
Engagement Score = AVERAGE('Attendance'[EngagementPoints])
Learning Score = AVERAGE('Attendance'[L&DPoints])
```

---

## 🧮 4. Performance Evaluation Dashboard
| Visual Type | X-Axis | Y-Axis / Value | Filters / Slicers | Table | Purpose |
|--------------|--------|----------------|--------------------|--------|----------|
| **Clustered Column Chart** | EmployeeID | QualityScore | Department | Evaluation | Compare evaluation quality |
| **Line Chart** | EvaluationDate | QualityScore | Department | Evaluation | Quality trend over time |
| **Donut Chart** | Department | Avg TimelySubmissionRate | — | Evaluation | On-time submission distribution |
| **Gauge Chart** | — | Performance Index | — | Combined | Overall team performance |
| **Table Visual** | Employee, QualityScore, TimelySubmissionRate | — | Department | Detailed view for managers |

**📘 DAX:**
```DAX
Timely Submission Rate = DIVIDE(COUNTROWS(FILTER('Evaluation', 'Evaluation'[SubmittedOnTime] = 1)), COUNTROWS('Evaluation'), 0) * 100
Quality Score = AVERAGE('Evaluation'[QualityScore])
```

---

## 💰 5. Revenue Analytics Dashboard
| Visual Type | X-Axis | Y-Axis / Value | Filters / Slicers | Table | Purpose |
|--------------|--------|----------------|--------------------|--------|----------|
| **Funnel Chart** | LeadStatus | LeadCount | ProductCategory | CRM | Lead progression from Open → Won |
| **Clustered Bar Chart** | InternID | RevenueGenerated | ProductCategory | CRM | Compare intern-wise revenue |
| **Line Chart** | LeadDate | RevenueGenerated | InternID | CRM | Monthly revenue trend |
| **Card Visuals** | — | Total Leads, Converted Leads, Conversion Rate | — | CRM | Quick revenue summary |
| **Tree Map** | ProductCategory | RevenueGenerated | — | CRM | Revenue distribution by product |

**📘 DAX:**
```DAX
Total Leads = COUNTROWS('CRM')
Converted Leads = COUNTROWS(FILTER('CRM', 'CRM'[LeadStatus] = "Closed Won"))
Conversion Rate = DIVIDE([Converted Leads], [Total Leads], 0) * 100
Total Revenue = SUM('CRM'[RevenueGenerated])
```

---

## 👥 6. Employee Summary Page
| Visual Type | X-Axis | Y-Axis / Value | Filters | Table | Purpose |
|--------------|--------|----------------|----------|--------|----------|
| **Table / Matrix** | FullName, Department, Role | ActiveHours, AttendanceRate, PerformanceIndex, RevenueGenerated | Date | Employee + all | Consolidated performance by individual |
| **Card Visuals** | — | Employee Name, Supervisor | — | Employee | Employee context |
| **Slicer Panel** | Department, Role, Date Range | — | — | — | Global filtering for all visuals |

---

## 🧠 Design & Layout Tips
- Use two rows of visuals per page (KPI cards on top, charts below).  
- Maintain consistent color theme:  
  - Productivity → Blue  
  - Attendance → Orange  
  - Performance → Green  
  - Revenue → Purple  
- Add navigation buttons between pages (Home, Productivity, Attendance, etc.).  
- Keep each chart title concise and metric-focused (e.g., “Weekly Active Hours Trend”).  
- Enable cross-filtering between visuals (clicking department updates all visuals).  
- Use tooltips for deeper insights (hover on bars to see details).  

---

## 📦 Suggested Dashboard Layout per Page
**Top Row (3–4 visuals):**  
➡ KPI Cards + Gauges  

**Middle Row:**  
➡ Trend Line / Bar / Column Charts  

**Bottom Row:**  
➡ Heatmap / Table + Department Filters  


