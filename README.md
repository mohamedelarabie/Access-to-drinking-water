# Investigating Global Access to Clean Drinking Water (UN SDG 6)

**Author:** Mohamed El Arabie  
**Project Workspace:** [Google Sheets Dashboard](https://docs.google.com/spreadsheets/d/1XP_JBwpINNsbu3Dhy2fF6Yx-VoJ-borj6_r16Efh5p8/edit?usp=sharing)  

## Project Overview
This data analysis project investigates global access to safe and affordable drinking water, aligning with the United Nations Sustainable Development Goal (SDG) 6. Using the WHO/UNICEF Joint Monitoring Programme (JMP) Estimates on the Use of Water dataset (2000–2020), the project involves extensive data cleaning, exploratory data analysis, transformation, and visualization to extract actionable insights regarding national, urban, and rural water access trends.

---

## Phase 1: Understanding and Cleaning the Data

### 1. Data Import and Integrity Checks
* **Importing & Delimiter Handling:** Imported the raw CSV data into Google Sheets. Identified instances where semicolon separators were mixed with commas, causing column misalignment. 
* **Row Validation:** Created a `value_cnt` feature using the `COUNTA()` function to count the number of populated cells per row. Applied filters to isolate rows with missing or shifted data (anything not equal to 16 columns) and fixed them using the **Split text to columns** tool.
* **Error Handling:** Handled `#VALUE!` errors and anomalous inputs (e.g., converting missing values to explicit text `"NAN"`).

### 2. Population Size Investigation
* **Global Benchmarking:** Compared the dataset's aggregated population values against the estimated 2020 global population (7.821 billion) and the global urban share (55%) using percentage differences.
* **Feature Engineering:**
    * Calculated `pop_u_val` (absolute urban population) and `pop_r` (rural population share) to complete the demographic breakdown.
    * To improve chart readability and mitigate outliers, created `pop_n (m)` to represent national populations rounded up to the nearest million.
* **Visualizations:** Plotted national population sizes versus urban/rural shares using smoothed line charts with aggregated averages to observe demographic distributions.

### 3. Measuring Central Tendency and Spread
* **Statistical Summaries:** Calculated the maximum, minimum, mean, median, mode, standard deviation, and interquartile range (IQR) for the four service levels: *At least basic, Limited, Unimproved, and Surface*.
* **Data Correction:** Identified unrealistic percentage values (>100%) in the basic access category and created a corrected `wat_bas_n (rounded)` feature. 
* **Visualizations:** Constructed candlestick charts (box-and-whisker plots) to visualize the distribution, median, and IQR of access levels across national, urban, and rural demographics. 

### 4. Analyzing Access by Population and Income
* **Income Group Mapping:** Converted text-based income groups into a numerical scale (Low=1, Lower middle=2, Upper middle=3, High=4) for analytical sorting. 
* **Pivot Tables:** Aggregated the sum of national populations and the average access shares across different income groups. 
* **Visualizations:** Created 100% stacked column charts to explore the relationship between population size/urbanization and service level distribution.

---

## Phase 2: Transforming the Data and Trend Analysis

### 1. Temporal Data Handling
* **Chronological Sorting:** Implemented advanced range sorting (by Country Name A to Z, then by Year A to Z) to ensure chronological sequential rows per country.
* **Year Difference (`y_diff`):** Engineered a feature to calculate the gap between recording years using conditional logic (`IF` the country name in row n matches row n+1).

### 2. Annual Rates of Change (ARC)
* **ARC Calculation:** Used the UN's standard ARC formula to measure the yearly change rate in basic water access. Created features for national (`ARC_n`), rural (`ARC_r`), and urban (`ARC_u`) populations.
    * *Formula used:* `IFERROR(IF($A3=$A2, (E3-E2)/($B3-$B2), ""), "null")`
* **Disparity Analysis:** Calculated `ARC_diff` to measure the exact percentage point difference in progress between rural and urban areas. 

### 3. "Full Access" Categorization
* **Thresholding:** Created `ARC_n_full`, `ARC_r_full`, and `ARC_u_full` using conditional logic to tag countries that had already achieved >99% (rounded to 100%) basic water access across both recorded years. This ensured that a 0% ARC in these nations was accurately interpreted as maintained perfection rather than stagnated progress.

### 4. Regional Groupings and Narrative Synthesis
* **Regional Integration:** Imported a secondary region dataset and mapped countries to their UN geographical regions using `LOOKUP` functions.
* **Data Storytelling:** Summarized ARC metrics and current access levels by region. The analysis culminated in a data-driven narrative focusing on the Sub-Saharan African water crisis, projecting that at current ARC trajectories, the region will only reach full access to basic water services by approximately the year 2080.
