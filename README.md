[View the Live Google Sheet Analysis Here](https://docs.google.com/spreadsheets/d/1XP_JBwpINNsbu3Dhy2fF6Yx-VoJ-borj6_r16Efh5p8/edit?gid=0#gid=0)




# Integrated Project: Access to Drinking Water (Understanding the Data)

## Project Overview
This project investigates global access to safe and affordable drinking water, supporting United Nations Sustainable Development Goal 6 (Clean water and sanitation). The analysis utilizes the WHO/UNICEF Joint Monitoring Programme (JMP) dataset (Estimates on the use of water, 2020) to identify inequalities in service levels across different countries, regions, and population sizes.

## 1. Data Import and Cleaning
The initial phase involved importing raw data and ensuring structural integrity.

* **Separator Correction:** Addressed formatting issues where semicolons were used instead of commas in specific rows (e.g., Croatia entries), causing column misalignment.
* **Data Validation:** Created a custom feature, `value_cnt`, using the `COUNTA()` function to verify that every row contained exactly 16 values (columns).
* **Error Correction:** Used filters to isolate rows with incorrect counts and applied `Data > Split text to columns` to fix the misalignment.

## 2. Feature Engineering
To facilitate deeper analysis, several new features were calculated and added to the dataset:

* **`pop_u_val`:** Calculated the absolute number of people living in urban areas (converting percentage share to a numerical value).
* **`pop_r`:** Calculated the rural population share percentage (assuming Urban + Rural = 100%).
* **`pop_n (m)`:** Rounded the national population size up to the nearest million to better aggregate data and handle outliers in visualizations.
* **`wat_bas_n (rounded)`:** Created to correct data entry errors where basic service levels exceeded 100%. Values > 100% were rounded or flagged as NAN.
* **Numeric Income Groups:** Converted text-based income classifications (Low, Lower-middle, etc.) into numeric values (1–4) to allow for logical sorting in charts.

## 3. Exploratory Data Analysis (EDA)

### A. Investigating Population Size
* **Global Comparison:** Compared the dataset's aggregated population against the estimated 2020 World Population (7.821 billion) to determine coverage accuracy.
* **Percentage Difference:** Calculated the percentage difference between the dataset values and global estimates for both total and urban populations.
* **Visualization:** Created a line chart comparing National Population vs. Urban/Rural Share. To address outliers and improve readability, the x-axis was aggregated using the `pop_n (m)` feature.

### B. Investigating Access by Area
* **Statistical Summary:** Calculated measures of central tendency (Mean, Median, Mode) and spread (Interquartile Range, Standard Deviation) for all 12 water access features.
* **Distribution Visualization:** Created Box and Whisker plots (Candlestick charts) for National, Urban, and Rural service levels to visualize the spread of data and identify the distribution of Basic, Limited, Unimproved, and Surface water access.

### C. Investigating Access by Population Size
* **Stacked Analysis:** Created three 100% Stacked Column Charts (National, Urban, and Rural) to observe how population size influences access levels.
* **Data grouping:** Used rounded population shares (`pop_u (rounded)` and `pop_r (rounded)`) on the x-axis to group countries effectively and identify trends in service provision relative to urbanization levels.

### D. Investigating Access by Income Group
* **Pivot Table Analysis:** Grouped the data by `income_group` to summarize the sum of the population and average access levels for urban and national sectors.
* **Economic Correlation:** Visualized the relationship between a country's Gross National Income (GNI) classification and their water access metrics to determine if higher income correlates with better sanitation services.

## 4. Key Business Questions Addressed
This analysis provides data-driven answers to the following business questions derived from the project objectives:

1.  **Data Representativeness:** What is the percentage difference between the dataset's coverage and the estimated 2020 global urban population size?
2.  **Population Trends:** Do national population sizes correlate with a 50/50 split between urban and rural residency?
3.  **Service Distribution:** Is the distribution of national basic water services more similar to urban basic services or national limited services?
4.  **Rural Variability:** What is the Interquartile Range (IQR) of rural surface water usage, and what does this variability indicate about rural infrastructure?
5.  **Urbanization Impact:** Do countries with higher urban population shares consistently provide better access to basic water services?
6.  **Rural Access:** Do countries with small rural populations consistently achieve 100% basic water access?
7.  **Economic Disparity (Low Income):** What is the average national access to limited water services specifically in Low-Income countries?
8.  **Demographic Distribution:** How is the global population distributed across income groups (e.g., do more people live in Low-Income or Middle-Income nations)?
9.  **Service by Economy:** Which income group (Low, Lower-Middle, Upper-Middle, High) has the highest prevalence of surface water usage?
10. **Global Correlations:** Does the data support the hypothesis that as GNI and urbanization increase, access to basic water increases while reliance on surface water decreases?
