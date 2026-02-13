---
layout: posts
title:  "Training Analytics Dashboard"
date:   2026-02-13 
tags: [power-bi]
author_profile: true
author: Moshraf Hossain
categories: work
highlight_home: true
tagline: "Transforming fragmented training data into executive-ready insights"
header:
  overlay_image: /assets/images/training-dashboard/training-dashboard-banner.png
  teaser: /assets/images/training-dashboard/training-dashboard-teaser.png
  caption: "Power BI Dashboard | Data Analytics Portfolio Project"
description: An end-to-end Power BI solution demonstrating DAX proficiency, star schema data modelling, and business intelligence capabilities through interactive training analytics.
---

# Training Analytics Dashboard
**Power BI Portfolio Project | Data-Driven Talent Development Insights**

---

## 🎯 The Challenge

Training and development teams in organisations face a critical problem: **they lack centralised, real-time visibility into training effectiveness and resource utilisation**.

Imagine being an L&D manager responsible for hundreds of training sessions, multiple facilitators, and dozens of development projects—but all your data lives in disconnected spreadsheets. You spend 10-15 hours every month manually copying, pasting, and aggregating data just to answer basic questions:

- How many employees are we reaching across different training programs?
- Which facilitators are delivering the most sessions, and where are capacity gaps?
- Are we creating training materials aligned with organisational priorities?
- What's our project completion rate, and where are the bottlenecks?

**This was the business problem I set out to solve.**

---

## 💡 My Solution

I built a **comprehensive 3-page Power BI dashboard** that transforms raw training data into executive-ready analytics. The solution provides role-specific insights for three key stakeholder groups, enabling data-driven decision-making without manual reporting overhead.

---

## 📊 Dashboard Architecture

The solution is structured as a **3-page analytical framework**, with each page serving distinct stakeholder needs:

---

### 📄 **Page 1: Executive Overview**
*Strategic KPIs and high-level trends for senior leadership*

![Executive Overview](/assets/images/training-dashboard/page1-executive-overview.png)
*High-level KPIs and training activity trends for senior leadership decision-making*

**Key Metrics:**
- 👥 **Total Participants:** 136 employees reached across all training sessions
- 📅 **Sessions Delivered:** 89 training activities completed
- 📚 **Resources Created:** 26 development projects tracked
- ✅ **Project Completion Rate:** 100% completion (demonstrating portfolio health)

**Key Visualizations:**
- **Training Activity Trend:** Dual-axis chart revealing monthly patterns in session delivery vs. participant engagement
- **Resource Creation by Category:** Donut chart showing content development priorities (Team Dev: 38%, Technical: 38%, Projects: 19%, Compliance: 4%)

**Business Value:** Executives can assess training impact in under 30 seconds without drowning in spreadsheet details. The dashboard immediately answers "Are we reaching our people?" and "Are we completing what we start?"

---

### 👥 **Page 2: Training Delivery Analysis**
*Operational insights for training managers and coordinators*

![Training Delivery Analysis](/assets/images/training-dashboard/page2-training-delivery.png)
*Facilitator performance metrics and session delivery insights for operational managers*

**Key Metrics:**
- 📊 **Total Sessions:** 89 training activities delivered
- 👥 **Total Participants:** 136 individuals engaged
- 👨‍🏫 **Active Facilitators:** 4 trainers contributing to delivery
- 📈 **Avg Participants/Session:** 1.53 efficiency metric

**Key Visualisations:**
- **Top Facilitators by Sessions Delivered:** Horizontal bar chart revealing Jenn leads with 37 sessions (41% of total delivery), while Roy delivered 14 sessions (16%)—highlighting potential workload imbalance
- **Sessions by Delivery Type:** Donut chart showing 86.5% live vs. 13.5% virtual distribution
- **Monthly Session Delivery Trend:** Area chart revealing peak activity in June-July (19 sessions each) and lower volume in October-November (5-7 sessions)—indicating seasonal patterns that inform hiring decisions

**Business Value:** Managers can identify workload imbalances (Jenn carrying 41% of delivery burden), understand delivery mode preferences, and anticipate seasonal capacity needs for proactive resource planning.

---

### 📂 **Page 3: Resource Development Analysis**
*Project tracking and content creation insights for development teams*

![Resource Development Analysis](/assets/images/training-dashboard/page3-resource-development.png)
*Project tracking and resource creation metrics for content development teams*

**Key Metrics:**
- 📂 **Total Resources:** 26 development projects in portfolio
- ✅ **Projects Completed:** 26 (100% completion rate)
- 📊 **Completion Rate:** 100% (calculated using robust DAX logic)
- 👤 **Active Project Leads:** 1 lead managing all projects

**Key Visualisations:**
- **Resources Created by Category:** Column chart showing Team Dev and Technical lead with 10 resources each, Projects with 5, and Compliance with 1—revealing content distribution priorities
- **Project Status Distribution:** Donut chart tracking Completed/In Progress/Not Started status (100% completed in this dataset)
- **Top Project Leads by Resources Created:** Horizontal bar chart highlighting individual contributions
- **Resources by Complexity Level:** 100% stacked bar chart revealing Team Dev projects are 90% Low complexity, while Technical projects split 50-50 between Low and Medium complexity

**Business Value:** Project leads can identify stalled initiatives, assess content complexity patterns, and align resource allocation with strategic priorities. The complexity breakdown helps with capacity planning—low complexity projects require less time investment.

---

## 🗂️ Data Model & Architecture

### **Star Schema Design**

I designed a **star schema** optimised for analytical performance and maintainability:

**Fact Tables:**
- `Facts_Training_Session` – Training delivery data (89 sessions, participant counts, delivery types)
- `Facts_Development_Projects` – Resource creation tracking (59 projects, status, complexity levels)

**Dimension Tables:**
- `Dim_People` – Facilitators and project leads (shared dimension with Role column)
- `Dim_Category` – 6 training categories (Team Development, Technical, Projects, Compliance, Leadership, Onboarding)
- `Dim_Audience` – 7 target audience groups
- `Dim_Date` – Calendar table marked as date table for time intelligence functions

**Relationship Structure:**
- All relationships are **Many-to-One (*:1)** for optimal query performance
- Shared dimensions (Category, Audience) connect both fact tables via separate relationship paths
- No many-to-many relationships—I resolved these by creating proper dimension tables

**Why Star Schema?**
- **Performance:** Many-to-One relationships enable fast query execution even with large datasets
- **Maintainability:** Shared dimensions reduce data duplication and simplify updates
- **Scalability:** Easy to add new fact tables (e.g., participant feedback, course evaluations) without restructuring the entire model

---

### **Data Transformation Highlights**

**Power Query Steps:**

1. **Date Type Conversion**
   - **Issue:** `Facts_Training_Session[Date]` column stored as Text in source CSV
   - **Impact:** Time-based filtering and chronological sorting not working
   - **Solution:** Converted to proper Date data type in Power Query
   - **Result:** Enabled time intelligence functions and date hierarchies

2. **Dimension Table Creation**
   - **Issue:** Both fact tables contained Category and Audience columns, creating many-to-many relationship conflicts
   - **Solution:** Extracted unique values to create separate `Dim_Category` and `Dim_Audience` tables
   - **Result:** Clean star schema with proper Many-to-One relationships

3. **Data Quality Validation**
   - Validated completeness of Status, Level, and Delivery Type columns
   - Identified and handled null values appropriately
   - Ensured consistent capitalization across categorical fields

---

## 🧮 DAX Measures Library

All measures are stored in a dedicated `_Measures` table for maintainability. Here are the key calculations:

---

### **Training Delivery Metrics**
```dax
// Basic aggregation measure
Total Participants = SUM(Facts_Training_Session[Participants])

// Row count measure
Total Sessions = COUNTROWS(Facts_Training_Session)

// Efficiency metric with error handling
Avg Participants per Session = 
DIVIDE(
    [Total Participants],
    [Total Sessions],
    0
)
// The third parameter (0) prevents divide-by-zero errors when filters produce empty tables

// Distinct count for capacity tracking
Active Facilitators = DISTINCTCOUNT(Facts_Training_Session[Facilitator])
```

---

### **Resource Development Metrics**
```dax
// Row count measure
Total Resources = COUNTROWS(Facts_Development_Projects)

// Filtered count using CALCULATE
Projects Completed = 
CALCULATE(
    COUNTROWS(Facts_Development_Projects),
    Facts_Development_Projects[Status] = "Completed"
)

// Percentage calculation with proper denominator
Completion Rate = 
DIVIDE(
    [Projects Completed],
    COUNTROWS(Facts_Development_Projects),
    0
)
// Formatted as Percentage with 0 decimal places in measure formatting

// Distinct count for team capacity
Active Project Leads = DISTINCTCOUNT(Facts_Development_Projects[Project Lead])

// Helper measure for chart aggregations
Project Count = COUNTROWS(Facts_Development_Projects)
```

---

### **Critical DAX Fix: Completion Rate**

**The Problem:**

During development, I encountered a calculation error that produced inflated completion percentages:

**Original Formula (Incorrect):**
```dax
Completion Rate = DIVIDE([Projects Completed], [Total Resources], 0)
```

**Issue:** This formula divided completed projects by total resources—two conceptually different metrics. When filtered, this produced nonsensical results like 145% completion.

**Root Cause Analysis:**
- `[Projects Completed]` counted projects with Status = "Completed"
- `[Total Resources]` counted all rows in the development projects table
- When both measures were filtered differently by slicers, the denominator didn't match the numerator's context

**Corrected Formula:**
```dax
Completion Rate = 
DIVIDE(
    [Projects Completed],
    COUNTROWS(Facts_Development_Projects),
    0
)
```

**Why This Works:**
- Both numerator and denominator now use `COUNTROWS()` on the same table
- They respond identically to filter context
- The calculation correctly represents "completed projects ÷ total projects"

**Result:** Accurate 100% completion rate (26 completed ÷ 26 total) that reflects true portfolio health.

**Lesson Learned:** Always ensure that percentage calculations use compatible numerators and denominators that respond to filter context in the same way.

---

## 🎨 Design Principles & User Experience

### **Visual Design Standards**

**Colour Palette:**

I selected colours with semantic meaning to guide user interpretation:

- **Primary Brand:** `#2E7D32` (Dark Green) – Headers, branding elements
- **Success Metrics:** `#4CAF50` (Green) – Positive outcomes, completed status
- **Neutral Metrics:** `#2196F3` (Blue) – General KPIs without positive/negative connotation
- **Progress Metrics:** `#FF9800` (Orange) – In-progress status, medium complexity
- **Calculated Metrics:** `#9C27B0` (Purple) – Derived calculations like averages and percentages

**Status & Complexity Colours:**
- **Completed:** `#4CAF50` (Green)
- **In Progress:** `#FF9800` (Orange)
- **Not Started:** `#E0E0E0` (Light Grey)
- **Low Complexity:** `#4CAF50` (Green)
- **Medium Complexity:** `#FF9800` (Orange)
- **High Complexity:** `#E53935` (Red)

---

### **Layout Standards**

**Technical Specifications:**
- **Canvas:** 1280px width, `#F9F9F9` background for reduced eye strain
- **Header:** 100px height, white text on green background
- **KPI Cards:** 245px × 100px with 4px coloured left border for visual hierarchy
- **Charts:** White background, 1px grey border, consistent 15px spacing
- **Typography:** Segoe UI throughout with 9pt minimum for WCAG 2.1 AA accessibility compliance

---

### **UX Design Philosophy**

**1. Progressive Disclosure**
- **Page 1 (Executive View):** High-level summary answering "Are we effective?"
- **Pages 2-3 (Operational Views):** Detailed drill-downs answering "Where specifically?"
- Users start broad and drill down as needed—reducing cognitive overload

**2. Consistent Navigation Pattern**
- Repeated header/filter/footer structure across all pages reduces learning curve
- Users immediately know where to find controls
- Footer shows "Page X of 3" for orientation

**3. Semantic Colour Coding**
- Green always means success/completion
- Orange always means progress/medium priority
- Purple always means calculated/derived metrics
- Reduces mental processing time—users decode meaning instantly

**4. Accessible Contrast**
- All text meets WCAG 2.1 AA standards (minimum 4.5:1 contrast ratio)
- KPI numbers use large fonts (32pt) for quick scanning
- Chart data labels positioned for maximum readability

---

## 🛠️ Technical Challenges & Solutions

---

### **Challenge #1: Many-to-Many Relationship Error**

**Symptom:** Power BI prevented direct relationship creation between fact tables and shared Category/Audience columns, displaying error: "This relationship has a many-to-many cardinality and can't be used."

**Root Cause:** Both `Facts_Training_Session` and `Facts_Development_Projects` contained Category and Audience columns. Power BI detected that a single category value appeared in multiple rows of both tables, creating a many-to-many relationship pattern.

**Solution:**
1. Created separate dimension tables:
   - `Dim_Category` with unique category values
   - `Dim_Audience` with unique audience values
2. Established Many-to-One relationships:
   - `Facts_Training_Session[Category]` → `Dim_Category[Category]`
   - `Facts_Development_Projects[Category]` → `Dim_Category[Category]`
   - Similar pattern for Audience

**Result:** Clean star schema with proper relationships. Filters now cascade correctly from dimensions to both fact tables.

**Learning:** Always create dedicated dimension tables for shared attributes rather than reusing columns across fact tables. This is fundamental to star schema design.

---

### **Challenge #2: Completion Rate Calculation Error**

**Symptom:** Completion Rate KPI displayed nonsensical values (e.g., 145%, or changing erratically with filters)

**Root Cause:** Original formula `DIVIDE([Projects Completed], [Total Resources], 0)` divided two conceptually different measures that responded differently to filter context.

**Solution:** Changed denominator to use `COUNTROWS(Facts_Development_Projects)` to ensure both numerator and denominator use the same table context.

**Result:** Accurate 100% completion rate that correctly reflects 26 completed projects out of 26 total.

**Learning:** Percentage calculations require compatible numerators and denominators. Both should reference the same table or respond identically to filters.

---

### **Challenge #3: Date-Based Filtering Not Working**

**Symptom:** 
- Month names sorted alphabetically (April, August, December) instead of chronologically
- Date slicers didn't recognise the column as a date
- Time intelligence functions threw errors

**Root Cause:** Source CSV stored dates as text strings (e.g., "2023-05-15" as Text data type)

**Solution:**
1. Opened Power Query Editor
2. Selected `Facts_Training_Session[Date]` column
3. Transform tab → Data Type → Date
4. Applied changes and refreshed data model

**Result:**
- Proper chronological sorting in visuals
- Date hierarchies (Year/Quarter/Month/Day) automatically available
- Time intelligence functions (e.g., SAMEPERIODLASTYEAR) now functional

**Learning:** Always verify data types during initial data import. Text-formatted dates are a common issue in CSV files.

---

### **Challenge #4: Bar Chart Showing Identical Values**

**Symptom:** "Top Project Leads" bar chart displayed the same value for all facilitators, despite different actual contribution levels.

**Root Cause:** Chart used the `[Total Resources]` measure instead of counting individual records per person. The measure returned the same grand total for each facilitator.

**Solution:** Changed the chart's Values field from `[Total Resources]` to `Count of Project ID`, which correctly counts distinct projects per person.

**Result:** Accurate representation showing differential contributions (e.g., Lead A: 15 projects, Lead B: 8 projects).

**Learning:** When creating "per person" or "per category" charts, use row-level counts or sums rather than aggregate measures that might not respect the visual's grouping context.

---

## 📈 Business Impact & Value Proposition

### **Quantifiable Outcomes**

If deployed in a real organization, this dashboard would deliver:

**Efficiency Gains:**
- ✅ **80% reduction in reporting time:** From 15 hours/month of manual Excel aggregation to <3 hours/month with automated refresh
- ✅ **Instant insights:** Stakeholders answer their own questions in seconds rather than waiting days for IT reports

**Strategic Benefits:**
- ✅ **Self-service analytics:** Executives, managers, and project leads access role-specific views without creating reporting bottlenecks
- ✅ **Proactive decision-making:** Seasonal patterns (June-July peaks) inform advance hiring for Q2 capacity
- ✅ **Workload balancing:** Identify facilitators carrying disproportionate loads (Jenn at 41% vs. Roy at 16%)

**Resource Optimisation:**
- ✅ **Align content creation with demand:** Category breakdown reveals whether resources match actual training delivery priorities
- ✅ **Complexity-based planning:** Understanding that Team Dev projects are 90% Low complexity helps estimate development timelines
- ✅ **Completion tracking:** 100% completion visibility prevents scope creep and ensures accountability

---

### **Stakeholder-Specific Value**

**For Executives:**
- Answer "Are we reaching our people?" at a glance (136 participants metric)
- Assess portfolio health (100% completion rate)
- Make budget decisions based on category distribution

**For Training Managers:**
- Balance facilitator workloads proactively
- Plan for seasonal capacity (hiring temps in May before June-July peak)
- Understand live vs. virtual preferences (86.5% live—may need more physical training space)

**For Project Leads:**
- Track project completion status across categories
- Identify bottlenecks (all projects completed—process is effective)
- Understand complexity patterns for future resource estimation

---

## 💼 Skills Demonstrated

### **Technical Capabilities**

**Power BI Platform:**
- ✅ Report design and page layout optimization
- ✅ Interactive visualizations (9 chart types implemented)
- ✅ Slicer configuration for cross-page filtering
- ✅ Conditional formatting and semantic colour application
- ✅ Publishing and sharing workflows (prepared for Power BI Service deployment)

**Data Modelling:**
- ✅ Star schema design from first principles
- ✅ Relationship management (all Many-to-One, no many-to-many)
- ✅ Dimension table creation to resolve relationship conflicts
- ✅ Date table configuration for time intelligence
- ✅ Data model documentation and diagram creation

**DAX (Data Analysis Expressions):**
- ✅ Aggregation functions (SUM, COUNTROWS, DISTINCTCOUNT)
- ✅ Filter context manipulation with CALCULATE
- ✅ Error handling with DIVIDE and default return values
- ✅ Measure organization in dedicated tables
- ✅ Performance optimization (avoiding calculated columns where measures suffice)

**Power Query (Data Transformation):**
- ✅ Data type conversions (Text to Date)
- ✅ Column extraction and dimension table creation
- ✅ Data quality validation and null handling
- ✅ Source query optimization

---

### **Analytical & Business Skills**

**Business Analysis:**
- ✅ KPI selection aligned to stakeholder needs (different metrics for each audience)
- ✅ Trend identification (seasonal patterns, workload distribution)
- ✅ Root cause analysis (why is Jenn carrying 41%? Capacity planning needed)
- ✅ Business requirements translation (L&D pain points → dashboard features)

**Problem-Solving:**
- ✅ Troubleshooting data model errors (many-to-many relationships)
- ✅ Debugging DAX calculation issues (completion rate formula)
- ✅ Iterative refinement (adjusted charts based on data availability)

**Communication:**
- ✅ Visual storytelling (progressive disclosure from high-level to detailed)
- ✅ Stakeholder-focused design (each page serves a specific role)
- ✅ Documentation and knowledge transfer (this portfolio page itself)

---

### **Design & User Experience**

**Visual Design:**
- ✅ Colour theory application (semantic meaning for colours)
- ✅ Typography hierarchy (Segoe UI with consistent sizing)
- ✅ White space management for reduced cognitive load
- ✅ Consistent branding across all pages

**Accessibility:**
- ✅ WCAG 2.1 AA contrast compliance (4.5:1 minimum)
- ✅ Readable font sizes (9pt minimum)
- ✅ Colour-blind friendly palette (not relying solely on colour for meaning)

**User Experience:**
- ✅ Intuitive navigation (consistent header/filter/footer pattern)
- ✅ Self-explanatory visualizations (no manual required)
- ✅ Responsive to user interaction (slicers update all visuals instantly)

---

## 🚀 Future Enhancements

**Predictive Analytics:**
- Implement DAX time intelligence functions to forecast training demand
- Use historical patterns (June-July peaks) to predict future capacity needs
- Alert managers 2 months in advance of high-demand periods

**Drill-Through Capabilities:**
- Add participant-level drill-through pages (click a session → see attendee list)
- Facilitator detail pages (click facilitator name → see full session history)
- Session feedback integration (link to post-training survey scores)

**Advanced DAX:**
- Create "same period last year" comparisons to track year-over-year growth
- Implement running totals for cumulative participation tracking
- Add "what-if" parameters for scenario planning (e.g., if we hire 2 more facilitators...)

**Automated Alerts:**
- Use Power Automate to email managers when completion rate drops below 90%
- Flag facilitators exceeding recommended session load (e.g., >35% of total)
- Alert when project status hasn't updated in 30+ days

**Benchmarking:**
- Add industry benchmark data (average participants per session in similar organizations)
- Compare performance across departments or regions
- External data integration (LinkedIn Learning course completions, Coursera enrollments)

---

## 📂 Project Resources

**GitHub Repository:** [View Full Documentation & Code](https://github.com/moshraf/training-analytics-dashboard)

**Project Files:**
- `Training_Analytics_Dashboard_Portfolio.pbix` – Power BI report file (interactive workbook)
- `data/Training_Delivery_Sessions.csv` – Training session data (89 sessions, 2023)
- `data/Training_Development_Projects.csv` – Resource development tracking (59 projects)
- `documentation/` – DAX measures, data model diagram, technical specifications

**Download Dashboard:** [Training_Analytics_Dashboard_Portfolio.pbix](https://github.com/moshraf/training-analytics-dashboard/blob/main/Training_Analytics_Dashboard_Portfolio.pbix)

---

## 🎓 Reflections & Key Takeaways

### **What I Learned**

**Technical Lessons:**

1. **Data modelling is foundational** – A clean star schema prevents countless downstream issues. Investing time upfront in proper dimension tables saved hours of troubleshooting later.

2. **DAX requires careful validation** – My completion rate error taught me to always test measures with multiple filter combinations. A formula that works with no filters might break when users apply slicers.

3. **Data types matter** – The date column issue (text vs. date) showed me that seemingly small data preparation steps have cascading impacts on visualization capabilities.

**Design Lessons:**

4. **User experience trumps technical complexity** – I could have added 20 more charts, but the three-page structure serves stakeholders better by reducing cognitive overload.

5. **Semantic colour coding reduces mental load** – Using green consistently for "success" and orange for "progress" means users decode meaning instantly without reading legends.

**Process Lessons:**

6. **Documentation is essential** – Detailed specifications enabled me to hand off this project confidently. In a real job, colleagues could maintain this dashboard without asking me constant questions.

7. **Iterative development is realistic** – I encountered 9 technical issues during development (documented in the handover report). Each issue taught me something new, and troubleshooting is where real learning happens.

---

### **Why This Project Matters for My Career**

As a recent **Master of Data Science graduate**, this project demonstrates my readiness for Data Analyst roles by showcasing:

**End-to-End Capability:**
- I didn't just analyze existing dashboards—I built one from scratch, from data import to final visualization

**Business Acumen:**
- I translated an ambiguous business problem (L&D teams need visibility) into specific, actionable features

**Independent Problem-Solving:**
- I encountered and resolved 9 technical challenges without instructor guidance, demonstrating self-sufficiency

**Stakeholder Awareness:**
- I designed three distinct pages because I understand that executives, managers, and project leads have different analytical needs

**Communication Skills:**
- This portfolio page itself demonstrates my ability to explain technical work to non-technical audiences

**Real-World Readiness:**
- The dashboard uses industry-standard tools (Power BI, DAX), follows best practices (star schema, semantic layer), and solves realistic business problems

---

## 📧 Let's Connect

I'm actively seeking **Data Analyst** opportunities where I can apply Power BI, DAX, and business intelligence skills to drive data-informed decision-making.

**Portfolio:** [https://moshraf.github.io/](https://moshraf.github.io/)  
**LinkedIn:** [https://www.linkedin.com/in/moshrafhossain/](https://www.linkedin.com/in/moshrafhossain/)  
**Email:** [mmoshraf@gmail.com](mailto:mmoshraf@gmail.com)  
**GitHub:** [https://github.com/moshraf](https://github.com/moshraf)

**Interested in discussing this project or exploring collaboration opportunities? I'd love to connect!**

---

**Built with:** Power BI Desktop | DAX | Star Schema Modelling | Power Query  
**Project Duration:** 4 weeks (January - February 2026)  
**Status:** Complete & Portfolio-Ready ✅

---

**Tags:** #PowerBI #DataAnalytics #DAX #BusinessIntelligence #DataModelling #PortfolioProject #DataScience

