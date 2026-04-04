# Phase 1 – Requirements and User Model Report
## Car Data App – Automotive Data Analysis System

**Course:** Human-Computer Interaction  
**Author:** Sebastian Rusin, Wojciech Armata, Patrycja Starzyk , Tomasz Bieńko
**Date:** April 2026

---

## Table of Contents

1. [Problem Definition](#1-problem-definition)
2. [Target User Group](#2-target-user-group)
3. [User Goals](#3-user-goals)
4. [Task Analysis](#4-task-analysis)
5. [Context of Use](#5-context-of-use)
6. [Personas](#6-personas)
7. [Task Hierarchy – Hierarchical Task Analysis](#7-task-hierarchy)
8. [Cognitive Demands of Tasks](#8-cognitive-demands-of-tasks)
9. [Potential Memory Load](#9-potential-memory-load)
10. [Possible User Errors](#10-possible-user-errors)
11. [Environmental Constraints](#11-environmental-constraints)

---

## 1. Problem Definition

### 1.1 Description of the Problem

The automotive resale market generates vast amounts of transactional data – prices, mileage, production year, fuel types, accident history, and more. For professionals working in car dealerships, automotive analysis, or academic research, making sense of this data without dedicated tooling is a significant challenge.

Spreadsheet software such as Microsoft Excel is commonly used but suffers from several limitations when dealing with automotive datasets:
- No integrated machine learning or price prediction capabilities
- Limited visual analytics (charts require manual configuration)
- No direct integration with external APIs (e.g., currency exchange rates)
- Poor usability for non-technical users when building custom filters or statistical summaries

The **Car Data App** addresses this gap by providing a desktop application that integrates data management, visualization, statistical analysis, and predictive modeling in a single, unified interface. The application loads structured CSV data, stores it in a local SQLite database, and exposes it through an interactive GUI built with Python's Tkinter framework.

### 1.2 Why the Problem Exists

The problem exists due to a gap between raw data availability and actionable insight. Automotive professionals often have access to structured export files (CSV, Excel), but lack either the technical knowledge to use data science tools (pandas, sklearn) or the time to build custom scripts. Off-the-shelf BI tools (Power BI, Tableau) are often too expensive, require cloud setup, or are too general-purpose for quick desktop use.

### 1.3 Why Solving It Matters

Providing a purpose-built desktop tool with Polish-language labels and pre-configured analyses reduces the technical barrier. It enables users to:
- Make faster, data-informed decisions about pricing
- Identify trends in the used car market
- Generate reports without writing code
- Predict fair market prices for specific vehicles

---

## 2. Target User Group

The application is targeted at a clearly defined and bounded user group with the following characteristics:

| Attribute | Description |
|---|---|
| **Age range** | 22–50 years old |
| **Professional background** | Automotive dealership staff, used-car market analysts, automotive business students |
| **Educational level** | Secondary education minimum; some university-level education expected |
| **Technical proficiency** | Low to intermediate – comfortable using desktop apps, email, spreadsheets; not necessarily programmers |
| **Physical constraints** | None specific; standard desktop or laptop use assumed |
| **Cognitive constraints** | May have limited statistical knowledge; rely on visual feedback rather than raw numbers |
| **Frequency of use** | Weekly or daily use, particularly during inventory assessments, reporting cycles, or purchasing decisions |

The group explicitly **excludes**:
- Data scientists or developers (they would use raw Python/pandas workflows)
- Casual end consumers browsing car listings (they use portals like OLX or AutoScout24)
- Enterprise-level fleet managers (they use ERP/CRM systems)

---

## 3. User Goals

### 3.1 Primary Goals

- **Understand the current state of car inventory or market data**: The user wants to quickly load data and see a structured table of all records.
- **Identify pricing patterns**: Determine which brands or fuel types command higher prices, and how mileage correlates with price.
- **Make a pricing decision for a specific car**: Use the price prediction feature to estimate the fair market value of a vehicle.

### 3.2 Secondary Goals

- Maintain data accuracy by adding, editing, or removing records.
- Export analytical results (charts as PNG, text analysis as TXT) for use in reports or presentations.
- Convert prices from USD to PLN using current exchange rates to localize data for the Polish market.
- Compare brands statistically (e.g., which brand has the lowest accident rate, highest average mileage).

### 3.3 Emotional and Experiential Goals

- **Feel in control**: Users want to feel that they can navigate the application without fear of breaking data or making irreversible mistakes.
- **Feel confident**: Statistical summaries and charts should reinforce the user's confidence in their pricing or purchasing decisions.
- **Reduce cognitive stress**: The system should present data clearly without requiring the user to mentally compute statistics.
- **Feel productive**: Tasks like generating a chart or running a prediction should take seconds, not minutes.

---

## 4. Task Analysis

### 4.1 Overview of User Tasks

Users of the Car Data App perform tasks that fall into four functional categories:

1. **Data loading and management** – getting data into the system and keeping it current
2. **Exploratory visual analysis** – understanding trends through charts
3. **Statistical investigation** – calculating and comparing metrics
4. **Predictive analysis** – estimating car prices using ML

### 4.2 High-Level Tasks

| # | Task | Description |
|---|---|---|
| T1 | Load data | Start the application and load CSV data into the table |
| T2 | Browse records | Scroll through the data table to inspect individual entries |
| T3 | Add / Edit / Delete records | Manage CRUD operations on individual records |
| T4 | Generate a chart | Select and display one of 10 available visualizations |
| T5 | View brand statistics | Compute specific metrics for a selected car brand |
| T6 | View descriptive analysis | Open the aggregated text-based analytics window |
| T7 | Convert currency | Update prices from USD to PLN via NBP API |
| T8 | Predict price | Enter vehicle parameters and obtain a price estimate |
| T9 | Export results | Save chart as PNG or analysis as TXT |

### 4.3 Subtasks and Micro-Operations

**T4 – Generate a Chart** (example breakdown):

- Open the application (application start)
  - Launch executable / run `app.py`
  - Wait for data to load from CSV
- Locate the chart controls in the button bar
  - Visually scan the bottom toolbar
  - Find the dropdown menu labeled "Wybierz wykres"
- Select a chart type
  - Click the dropdown
  - Read through the 10 available options
  - Select desired option (e.g., "Rozkład cen")
- Trigger display
  - Click the "Pokaż wykres" button
  - Wait for chart window to open
- Interpret chart
  - Read axis labels
  - Identify pattern or outlier
- Optionally save
  - Click "Zapisz jako PNG"
  - Choose file location in dialog
  - Confirm save

**T8 – Predict Price** (example breakdown):

- Click "Predykcja" button
- New window opens
- Enter brand name (text field, case-sensitive)
- Enter production year (integer)
- Enter mileage (integer)
- Enter accident history ("Yes" or "No")
- Click "Oblicz cenę"
- Read result in popup dialog

---

## 5. Context of Use

### 5.1 Physical Environment

The application is designed for **desktop use** in an indoor environment. Typical locations:
- Office desk at a car dealership (primary use case)
- University computer lab or personal laptop (academic/student use)
- Home office during remote analysis work

The application is a Tkinter GUI running natively on Windows. It is not a web or mobile application and is not designed for touchscreen use.

### 5.2 Technical Environment

| Parameter | Specification |
|---|---|
| **Platform** | Windows desktop (Windows 10/11) |
| **Screen size** | 1366×768 minimum; 1920×1080 recommended |
| **Connectivity** | Internet required only for currency conversion (NBP API) |
| **Input devices** | Mouse and keyboard |
| **Dependencies** | Python 3.x, pandas, matplotlib, seaborn, sklearn, requests |
| **Local storage** | SQLite database (`cars.db`) stored locally |

### 5.3 Social Environment

- Most users work **alone** or with a colleague nearby.
- In a dealership context, users may be interrupted by customers or phone calls during analysis.
- In academic settings, the application may be demonstrated to a group (presentation mode).
- No multi-user collaboration is supported; the database is single-user only.

### 5.4 Time Pressure and Interruptions

- Dealership staff may need quick answers during customer consultations (high time pressure).
- Analysts working on weekly reports have more time and focus (low time pressure).
- Interruptions are moderate to high in dealership environments.
- The application does not auto-save in real time; unsaved changes can be lost on crash.

---

## 6. Personas

### Persona 1 – Marek Wiśniewski

| Attribute | Details |
|---|---|
| **Age** | 38 |
| **Occupation** | Used car dealership manager, Warsaw |
| **Education** | Technical secondary school, automotive specialization |
| **Technical proficiency** | Moderate – uses Excel and email daily; has never written code |
| **Device** | Windows 11 desktop PC with a 24" monitor |

**Background:**  
Marek has been managing a used car dealership for 12 years. He buys 20–40 cars per month and needs to price them competitively without losing margin. He currently uses Excel to track inventory but finds it slow when he wants to compare brands or visualize trends.

**Goals:**
- Quickly find out the average market price for a specific brand and year
- See which fuel types are most popular in his inventory
- Predict a fair resale price before purchasing a car at auction

**Frustrations:**
- Excel charts require too many clicks and manual configuration
- He often forgets which formula he used for price calculations
- Currency conversion is done manually by checking Google

**Typical Usage Scenario:**  
Before buying a used BMW at auction, Marek opens the app, checks the average price for BMW in the dataset, views the "Price vs Mileage" scatter plot, and uses the price predictor with the car's specific parameters. The whole process takes 3–5 minutes.

**Skills and Limitations:**
- Strong domain knowledge of car values and market
- Limited statistical knowledge (does not understand correlation coefficients intuitively)
- Reads Polish fluently; limited English proficiency

---

### Persona 2 – Karolina Nowak

| Attribute | Details |
|---|---|
| **Age** | 23 |
| **Occupation** | 3rd-year student, Data Science, AGH University, Kraków |
| **Education** | Undergraduate (in progress) |
| **Technical proficiency** | High – uses Python, pandas, Jupyter Notebooks regularly |
| **Device** | 15.6" laptop, Windows 11, 1920×1080 |

**Background:**  
Karolina is working on a semester project analyzing the used car market in Central Europe. She was given a CSV dataset and needs to produce a report with charts and statistics. She knows how to code but prefers not to rebuild everything from scratch when a tool already exists.

**Goals:**
- Rapidly generate multiple charts for her report
- Export PNG images to include in her presentation
- Analyze brand-level statistics without writing custom groupby queries

**Frustrations:**
- Wants to customize chart colors and fonts (the app doesn't support this)
- Finds that some column names are in English while the UI is in Polish — slight inconsistency
- Would prefer a dark mode for late-night work sessions

**Typical Usage Scenario:**  
Karolina opens the application, selects all 10 chart types one by one, exports the most relevant ones as PNG, then opens the "Analizy opisowe" window, copies the text summary, and pastes it into her LaTeX report.

**Skills and Limitations:**
- Comfortable with data interpretation and statistical concepts
- May attempt to find features that don't exist (e.g., filtering the table by column)
- Works late at night under time pressure before deadlines

---

## 7. Task Hierarchy

### HTA for Task T8: Predict the Price of a Car

```
0. Predict the price of a specific car
   1. Open the application
      1.1 Launch app.py
      1.2 Wait for CSV data to load into table
      1.3 Confirm application is ready (table is populated)
   2. Initiate the prediction module
      2.1 Locate the "Predykcja" button in the toolbar
      2.2 Click the button
      2.3 Wait for the prediction window to open
   3. Enter vehicle parameters
      3.1 Type the car brand in the "Marka" field
          3.1.1 Identify correct brand spelling (case-sensitive)
          3.1.2 Type the brand name
      3.2 Type the production year in the "Rok produkcji" field
          3.2.1 Enter a valid 4-digit year
      3.3 Type the mileage in the "Przebieg (km)" field
          3.3.1 Enter a non-negative integer
      3.4 Type accident history in the "Wypadek" field
          3.4.1 Enter exactly "Yes" or "No"
   4. Submit prediction
      4.1 Click "Oblicz cenę"
      4.2 Wait for the result dialog to appear
   5. Interpret result
      5.1 Read the estimated price in the dialog
      5.2 Compare with own market knowledge
      5.3 Close dialog
   6. Optionally repeat with different parameters
      6.1 Modify one or more fields
      6.2 Re-submit
```

**Plan notation:**  
- Step 0: Do 1–2–3–4–5, then optionally 6
- Step 3: Do 3.1–3.2–3.3–3.4 in order; all fields are required
- Step 3.1: Do 3.1.1 before 3.1.2

---

## 8. Cognitive Demands of Tasks

### 8.1 Attention Requirements

| Task | Attention Level | Rationale |
|---|---|---|
| Loading data | Low | Automatic on startup |
| Browsing table | Moderate | Requires scanning rows; horizontal scrolling may be needed |
| Generating chart | Low | Two-click process with a dropdown |
| Entering prediction parameters | High | Four fields with specific format requirements |
| Interpreting statistical output | High | Requires domain knowledge to draw conclusions |
| CRUD operations | Moderate | Must identify correct row before editing/deleting |

### 8.2 Multitasking Involvement

Users in dealership contexts frequently multitask – answering phone calls or speaking with clients while using the application. This increases the risk of data entry errors, particularly during the prediction task (which requires typed input across four fields).

Karolina (Persona 2) may switch between the application and her report document simultaneously, increasing the chance of confusion between datasets.

### 8.3 Decision-Making Complexity

The most cognitively demanding decisions involve:
- **Choosing the right chart** from 10 options with similar-sounding names (e.g., "Korelacja cech liczbowych z ceną" vs. "Macierz korelacji")
- **Interpreting the price prediction** – users must judge whether the ML-generated result is plausible
- **Deciding to delete a record** – the action is irreversible within the session if the user doesn't re-import from CSV

### 8.4 Perception Requirements

- All critical information is presented **visually** (table, charts, dialogs)
- No auditory feedback is used by the application
- Small font sizes in the data table may cause strain for users with reduced visual acuity
- Chart labels and axis values must be readable – a challenge on smaller screens

---

## 9. Potential Memory Load

### 9.1 Information Users Must Remember

- The **exact brand name** as it appears in the dataset (for the prediction feature) — this relies on **recall** rather than recognition, which increases cognitive load
- The **format required** for the "Wypadek" field: must be exactly "Yes" or "No" (case-sensitive in the underlying code)
- The **location of buttons** in the toolbar — there is no persistent navigation menu or tooltips on all controls

### 9.2 Steps That Rely on Recall

- Typing a brand name in the prediction window without an autocomplete or dropdown forces the user to recall the exact spelling
- There are no visual reminders within the form about what format is expected for each field
- After closing the analysis window, users must remember key statistics if they want to reference them elsewhere

### 9.3 Working Memory Overload Risks

When using the statistics window, users must:
1. Select a brand from a list
2. Select a metric from a second list
3. Click "Oblicz"
4. Read and remember the result
5. Change one parameter and repeat

This sequential process without any side-by-side comparison view requires users to hold previous results in working memory, which becomes difficult when comparing more than 2–3 brands.

### 9.4 Design Assessment

The current design **increases** memory burden in the following areas:
- Free-text brand input in the prediction form
- No persistent display of previously computed statistics
- No summary panel showing currently loaded dataset information

---

## 10. Possible User Errors

### 10.1 Slips (Execution Errors)

| Error | Trigger | Consequence |
|---|---|---|
| Clicking "Usuń zaznaczony" instead of "Edytuj zaznaczony" | Buttons are adjacent in the toolbar | Record deleted unintentionally; no undo available |
| Typing brand name with wrong capitalization in prediction | "toyota" instead of "Toyota" | "Brand not found" error message |
| Entering a negative mileage value | Mistyping or copy-paste issue | Prediction may return nonsensical result |
| Pressing "Pokaż wykres" without selecting chart type | Forgetting to choose from dropdown first | Error or default "Wybierz wykres" selected |

### 10.2 Mistakes (Planning Errors)

| Error | Description |
|---|---|
| Expecting to filter the table | Users may look for a search/filter feature that does not exist |
| Assuming data is auto-saved | Users may close the app without clicking "Zapisz do bazy" and lose edits |
| Misinterpreting correlation coefficient | Users without statistical background may not understand what a 0.4 correlation means |
| Expecting undo functionality | No Ctrl+Z available; no undo stack implemented |

### 10.3 Confusions Caused by Labeling

- The button "Zapisz do bazy" suggests saving to the database, but it is not immediately clear this is separate from saving to the CSV file — users may not realize the CSV is the primary data source
- "Analizy opisowe" (descriptive analysis) and "Statystyki marki" (brand statistics) may seem to overlap — users may not know which one to use for a given question
- The chart option "Korelacja cech liczbowych z ceną" vs. "Macierz korelacji" may confuse users since both involve correlation

---

## 11. Environmental Constraints

### 11.1 Noise

In a dealership showroom, background noise from customers, phones, and vehicles can disrupt concentration. During multi-step tasks such as price prediction (requiring 4 typed inputs), noise-induced interruptions may cause users to lose their place or forget a value they were about to enter.

**Impact:** Medium — increases error rate in data entry tasks.

### 11.2 Lighting

The application uses a default light-gray Tkinter theme. In bright sunlight or near windows, the low-contrast interface may be hard to read. There is no dark mode.

**Impact:** Low to medium — screen glare is manageable with monitor positioning, but older users may struggle with default font sizes.

### 11.3 Mobility

The application is a desktop-only tool and cannot be used on mobile devices or tablets. It requires a mouse and keyboard. This limits use to fixed workstations.

**Impact:** High in mobile/field scenarios — a salesperson walking the car lot cannot use this tool on a phone.

### 11.4 Distractions and Interruptions

Dealership staff are frequently interrupted. The application has no session recovery mechanism — if the user walks away mid-task, no state is preserved between sessions unless data was explicitly saved to the database.

**Impact:** Medium — unsaved edits are particularly at risk.

### 11.5 Stress

When a purchasing decision must be made quickly (e.g., at an auction with a countdown timer), high stress may push users to skip steps or enter approximate values. The prediction model may return misleading results if given inaccurate inputs under pressure.

**Impact:** High — the prediction feature is most useful precisely in high-pressure scenarios, but is also most vulnerable to input errors in those moments.

---

## Summary

The Car Data App addresses a real and documented gap in the tooling available to automotive market professionals and students. Its target users are non-programmers with moderate technical proficiency who need data insights without coding. The primary interaction challenges involve:

- **Data entry accuracy** in the prediction module (recall-heavy, no input assistance)
- **Decision complexity** in chart selection (10 similar options, no preview)
- **Irreversibility** of delete actions
- **Memory burden** in comparative statistical analysis

Addressing these issues in subsequent design phases — through better input guidance, undo functionality, persistent comparison panels, and improved labeling — would substantially improve usability for both Marek and Karolina's use cases.

---
