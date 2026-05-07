# 📊 Student Performance Analysis – Power BI Dashboard

A multi-page Power BI dashboard for analyzing student academic performance, attendance, and behavior using a Star Schema data model.

---

## 📁 Project Structure

```
StudentPerformanceDashboard/
├── StudentPerformance.pbix        # Main Power BI file
├── Data/
│   ├── Students.csv               # Dimension table
│   ├── Scores.csv                 # Fact table
│   ├── Attendance.csv             # Fact table
│   └── Behavior.csv               # Fact table
└── README.md
```

---

## 🗂️ Dashboard Pages

| Page | Description |
|------|-------------|
| **Home** | Landing page with navigation buttons |
| **Academic Dashboard** | KPI cards, score by subject/class, term trend, student table |
| **Behavior Dashboard** | Donut chart + bar chart of behavior types |
| **Attendance Dashboard** | Dual-axis line/area chart of attendance % by month |
| **Student Profile** | Drillthrough page with individual student KPIs |
| **Tooltips** | Custom tooltip page (Average Score, Attendance %, Score distribution) |

---

## 🧩 Data Model

**Star Schema:**

```
Students (Dimension)
    │
    ├──► Scores      (Fact) — One-to-Many on StudentID
    ├──► Attendance  (Fact) — One-to-Many on StudentID
    └──► Behavior    (Fact) — One-to-Many on StudentID
```

Cross-filter direction: **Single**

---

## 🔧 Data Cleaning (Power Query)

### Column Naming Conventions

| Raw Name | Cleaned Name |
|----------|-------------|
| `student_id` | `StudentID` |
| `max_score` | `MaxScore` |
| `exam_type` | `ExamType` |

### Data Types

**Students Table**

| Column | Type |
|--------|------|
| StudentID | Whole Number |
| Name | Text |
| Gender | Text |
| Class | Whole Number |
| Section | Text |

**Scores Table**

| Column | Type |
|--------|------|
| Score | Decimal/Whole |
| MaxScore | Whole Number |
| Subject | Text |
| Term | Text |

**Attendance Table**

| Column | Type |
|--------|------|
| Date | Date |
| Status | Text |

**Behavior Table**

| Column | Type |
|--------|------|
| Date | Date |
| BehaviorType | Text |

### Null Value Handling

| Column | Replace Null With |
|--------|------------------|
| Reason | `"Unknown"` |
| Notes | `"No Notes"` |
| Score | `0` |

---

## 📐 DAX Measures

```dax
-- Percentage Score
% Score =
DIVIDE(SUM(Scores[Score]), SUM(Scores[MaxScore]), 0) * 100

-- Average Score per Subject
Average Score per Subject = AVERAGE(Scores[Score])

-- Attendance Measures
Present Days =
CALCULATE(COUNT(Attendance[Status]), Attendance[Status] = "Present")

Total Attendance = COUNT(Attendance[Status])

Attendance % = DIVIDE([Present Days], [Total Attendance], 0) * 100

-- Behavior Count
Behavior Count = COUNT(Behavior[BehaviorType])

-- KPI Measures
Total Students = DISTINCTCOUNT(Students[StudentID])
Avg Attendance = AVERAGE([Attendance %])
Avg Score = AVERAGE(Scores[Score])

-- Performance Category
Performance Category =
SWITCH(
    TRUE(),
    [% Score] >= 80, "High",
    [% Score] >= 50, "Medium",
    "Low"
)
```

> 💡 **Tip:** Store all measures in a dedicated empty table: `Measures = {}`

---

## 📊 Visualizations

### Page 1 – Academic Dashboard
- **KPI Cards:** Total Students (1000), Attendance % (90.05), Avg Score per Subject (49.87)
- **Stacked Bar Chart:** Average Score by Subject and Class (Classes 1–12)
- **Line Chart:** Sum of Score by Term (Term 1, 2, 3)
- **Table:** Student Name, Subject, Sum of Score, % Score with conditional formatting

### Page 2 – Behavior Dashboard
- **Donut Chart:** Count of StudentID by BehaviorType (equal ~20% each)
- **Bar Chart:** Behavior Count by BehaviorType (Disruptive, Late, Helpful, Participative, Absent without notice)

### Page 3 – Attendance Dashboard
- **Dual-Axis Chart:** Attendance % (line, red) + Count of Status (area, blue) by Month

### Page 4 – Student Profile *(Drillthrough)*
- **KPI Cards:** Behavior Count, Attendance %, Sum of Score
- **Area Chart:** Attendance % by Year, Quarter, Month
- **Bar Chart:** Behavior Count by BehaviorType

### Page 5 – Tooltips
- Average Score per Subject
- Attendance %
- Count of StudentID by Score (sparkline)

---

## 🔍 Slicers

All pages include synced slicers:
- **Class** (range slider: 1–12)
- **Section** (dropdown)
- **Subject** (dropdown)
- **Term** (dropdown)

---

## 🔗 Drillthrough Setup

1. Create a page named **Student Profile**
2. Add `Students[Name]` to the **Drillthrough Filters** field well
3. Right-click any student name on other pages → **Drillthrough → Student Profile**

---

## 🎨 Color Theme

| Performance | Color |
|-------------|-------|
| High (≥ 80%) | 🟢 Green |
| Low (< 40%) | 🔴 Red |

---

## 🔖 Bookmark Navigation

| Bookmark | Page |
|----------|------|
| Academic View | Academic Dashboard |
| Attendance View | Attendance Dashboard |
| Behavior View | Behavior Dashboard |

Buttons are assigned via: **Format → Action → Type: Bookmark**

---

## 📱 Mobile Layout

Arranged via **View → Mobile Layout:**
1. KPI Cards — top
2. Charts — middle
3. Slicers — bottom

---

## ⚠️ Common Errors & Fixes

| Error | Fix |
|-------|-----|
| Wrong relationship direction | Always use **One-to-Many** from Students |
| % Score returning blank | Use `DIVIDE()` instead of `/` |
| Filters not working | Check: relationship active? Correct cross-filter? Same data types? |

---

## ✅ Project Checklist

- [x] Data Cleaning
- [x] Star Schema Relationships
- [x] DAX Measures
- [x] KPI Cards
- [x] Charts (Bar, Line, Donut, Area)
- [x] Slicers
- [x] Drillthrough Page
- [x] Tooltips
- [x] Bookmark Navigation
- [x] Mobile Layout

---

## 🛠️ Tools Used

- **Power BI Desktop**
- **Power Query** (data transformation)
- **DAX** (measures and calculated columns)