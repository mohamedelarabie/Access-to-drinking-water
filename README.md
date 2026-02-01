[View the Live Google Sheet Analysis Here](https://docs.google.com/spreadsheets/d/1XP_JBwpINNsbu3Dhy2fF6Yx-VoJ-borj6_r16Efh5p8/edit?gid=0#gid=0)




# Integrated Project: Access to Drinking Water (Understanding the Data)

## Project Overview
[cite_start]This project investigates global access to safe and affordable drinking water, supporting **United Nations Sustainable Development Goal 6** (Clean water and sanitation)[cite: 5, 106]. [cite_start]The analysis utilizes the **WHO/UNICEF Joint Monitoring Programme (JMP)** dataset (Estimates on the use of water, 2020) to identify inequalities in service levels across different countries, regions, and population sizes[cite: 33, 97].

## 1. Data Import and Cleaning
The initial phase involved importing raw data and ensuring structural integrity.

* [cite_start]**Separator Correction:** Addressed formatting issues where `semicolons` were used instead of commas in specific rows (e.g., Croatia entries), causing column misalignment[cite: 215, 216].
* [cite_start]**Data Validation:** Created a custom feature, `value_cnt`, using the `COUNTA()` function to verify that every row contained exactly 16 values (columns)[cite: 225, 238].
* [cite_start]**Error Correction:** Used filters to isolate rows with incorrect counts and applied `Data > Split text to columns` to fix the misalignment[cite: 244].

## 2. Feature Engineering
To facilitate deeper analysis, several new features were calculated and added to the dataset:

* [cite_start]**`pop_u_val`:** Calculated the absolute number of people living in urban areas (converting percentage share to a numerical value)[cite: 285].
* [cite_start]**`pop_r`:** Calculated the rural population share percentage (assuming Urban + Rural = 100%)[cite: 327, 329].
* [cite_start]**`pop_n (m)`:** Rounded the national population size up to the nearest million to better aggregate data and handle outliers in visualizations[cite: 375].
* **`wat_bas_n (rounded)`:** Created to correct data entry errors where basic service levels exceeded 100%. [cite_start]Values > 100% were rounded or flagged as `NAN`[cite: 438, 452].
* [cite_start]**Numeric Income Groups:** Converted text-based income classifications (Low, Lower-middle, etc.) into numeric values (1–4) to allow for logical sorting in charts[cite: 682].

## 3. Exploratory Data Analysis (EDA)

### A. Investigating Population Size
* [cite_start]**Global Comparison:** Compared the dataset's aggregated population against the estimated 2020 World Population (7.821 billion) to determine coverage accuracy[cite: 276, 279].
* [cite_start]**Percentage Difference:** Calculated the percentage difference between the dataset values and global estimates for both total and urban populations[cite: 305].
* **Visualization:** Created a line chart comparing **National Population** vs. **Urban/Rural Share**. [cite_start]To address outliers and improve readability, the x-axis was aggregated using the `pop_n (m)` feature[cite: 323, 378].

### B. Investigating Access by Area
* [cite_start]**Statistical Summary:** Calculated measures of central tendency (Mean, Median, Mode) and spread (Interquartile Range, Standard Deviation) for all 12 water access features[cite: 461, 466].
* [cite_start]**Distribution Visualization:** Created **Box and Whisker plots (Candlestick charts)** for National, Urban, and Rural service levels to visualize the spread of data and identify the distribution of "Basic," "Limited," "Unimproved," and "Surface" water access[cite: 478].

### C. Investigating Access by Population Size
* [cite_start]**Stacked Analysis:** Created three **100% Stacked Column Charts** (National, Urban, and Rural) to observe how population size influences access levels[cite: 546, 550].
* [cite_start]**Data grouping:** Used rounded population shares (`pop_u (rounded)` and `pop_r (rounded)`) on the x-axis to group countries effectively and identify trends in service provision relative to urbanization levels[cite: 632, 645].

### D. Investigating Access by Income Group
* [cite_start]**Pivot Table Analysis:** Grouped the data by `income_group` to summarize the sum of the population and average access levels for urban and national sectors[cite: 678, 680].
* [cite_start]**Economic Correlation:** Visualized the relationship between a country's Gross National Income (GNI) classification and their water access metrics to determine if higher income correlates with better sanitation services[cite: 681, 750].

## 4. Key Business Questions Addressed
This analysis provides data-driven answers to the following business questions derived from the project objectives:

1.  [cite_start]**Data Representativeness:** What is the percentage difference between the dataset's coverage and the estimated 2020 global urban population size? [cite: 770]
2.  [cite_start]**Population Trends:** Do national population sizes correlate with a 50/50 split between urban and rural residency? [cite: 771]
3.  [cite_start]**Service Distribution:** Is the distribution of national basic water services more similar to urban basic services or national limited services? [cite: 772]
4.  [cite_start]**Rural Variability:** What is the Interquartile Range (IQR) of rural surface water usage, and what does this variability indicate about rural infrastructure? [cite: 774]
5.  [cite_start]**Urbanization Impact:** Do countries with higher urban population shares consistently provide better access to basic water services? [cite: 779, 780]
6.  [cite_start]**Rural Access:** Do countries with small rural populations consistently achieve 100% basic water access? [cite: 786]
7.  [cite_start]**Economic Disparity (Low Income):** What is the average national access to *limited* water services specifically in Low-Income countries? [cite: 787]
8.  [cite_start]**Demographic Distribution:** How is the global population distributed across income groups (e.g., do more people live in Low-Income or Middle-Income nations)? [cite: 792]
9.  [cite_start]**Service by Economy:** Which income group (Low, Lower-Middle, Upper-Middle, High) has the highest prevalence of surface water usage? [cite: 798]
10. [cite_start]**Global Correlations:** Does the data support the hypothesis that as GNI and urbanization increase, access to basic water increases while reliance on surface water decreases? [cite: 811]
