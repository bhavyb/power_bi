Student Performance Analysis Dashboard (Power BI)

This project is a Power BI dashboard created to analyze student performance using academic scores, attendance records, and behavior data. The dashboard helps track overall student progress and provides insights at both class level and individual student level.

Project Files
StudentPerformanceDashboard/
│
├── StudentPerformance.pbix
├── Data/
│   ├── Students.csv
│   ├── Scores.csv
│   ├── Attendance.csv
│   └── Behavior.csv
└── README.md

Dashboard Overview
The report contains multiple pages to analyze different aspects of student data.

1. Home Page
The home page is used for navigation between dashboards using buttons and bookmarks.

<img width="1377" height="786" alt="image" src="https://github.com/user-attachments/assets/2ac5e6cb-b267-4f5e-bd3f-eeb1e686760d" />


2. Academic Dashboard
This page focuses on academic performance.
Visuals included:
KPI cards for:
Total Students
Average Attendance %
Average Score
Subject-wise performance analysis
Score trends across terms
Student-level score table with conditional formatting

<img width="1373" height="789" alt="image" src="https://github.com/user-attachments/assets/2fce9d1b-a88e-4b19-b68e-30b4ab865f2f" />


3. Behavior Dashboard
This page shows student behavior patterns.
Visuals included:
Donut chart for behavior categories
Bar chart showing frequency of different behavior types

<img width="1374" height="775" alt="image" src="https://github.com/user-attachments/assets/d73cf92e-dc8f-4bf3-a6a8-0512a7990eb1" />


4. Attendance Dashboard
This page tracks attendance trends over time.
Visuals included:
Attendance percentage by month
Total attendance records by month using a combined chart

<img width="1387" height="788" alt="image" src="https://github.com/user-attachments/assets/fdbc574d-c160-4b3b-99af-821d652d8f43" />


5. Student Profile (Drillthrough Page)
A detailed page for individual student analysis.
Visuals included:
Attendance %
Total Score
Behavior Count
Monthly attendance trend
Behavior breakdown

<img width="1383" height="779" alt="image" src="https://github.com/user-attachments/assets/5129ffb4-4a23-41bd-9507-7a1e97696fa4" />

6. Tooltip Page
Custom tooltips were added to improve user interaction and display quick insights such as:
Average score
Attendance percentage

<img width="497" height="349" alt="image" src="https://github.com/user-attachments/assets/5299e7d2-4360-4c16-b99a-0983a9a1adcd" />



Relationships were created using StudentID with one-to-many relationships from the Students table to all fact tables.
Cross-filter direction was kept single to avoid ambiguity.
Data Cleaning in Power Query
Several transformations were applied before building the report.
Some column names were standardized for consistency.


Correct data types were assigned such as:
Whole Number
Text
Date
Null Value Handling
Missing values were replaced where required:
Missing scores replaced with 0
Empty notes replaced with "No Notes"
Missing reasons replaced with "Unknown"
DAX Measures Used

Some important measures created in the report are shown below.
% Score = DIVIDE(SUM(Scores[Score]), SUM(Scores[MaxScore]), 0) * 100

Attendance % = DIVIDE([Present Days], [Total Attendance], 0) * 100

Behavior Count = COUNT(Behavior[BehaviorType])

Total Students = DISTINCTCOUNT(Students[StudentID])

Additional measures were created for KPIs and analysis.

Filters and Slicers
The report includes slicers for:
Class
Section
Subject
Term

These slicers were synced across pages for easier navigation and filtering.
Drillthrough Feature
A drillthrough page was created for student-level analysis.
Users can right-click a student name from another visual and open the detailed Student Profile page.

Design Choices
Conditional formatting was used to highlight performance levels.
Green color represents high performance.
Red color represents low performance.
Bookmarks and buttons were added for navigation between pages.
Challenges Faced

Conclusion
This dashboard provides a simple way to monitor student performance across academics, attendance, and behavior. It can help teachers or school management identify trends, track student progress, and make better decisions using data visualization.
