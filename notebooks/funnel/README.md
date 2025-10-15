# Funnel Analysis Process

<div align='center'>

This document contains the process for creating analysis, including conversion and visuals. Our funnel tracks unique clients with thresholds for average session time and energy efficiency.

</div>

### **Roles:**

**Rolando:** Coding the Funnel

**Kabbo:** Visualizing the Funnel

***

## 1. Coding The Funnel

<div align='center'>

After we read the CSVs with the new feature engineering, we can begin to create the steps needed for our funnel analysis. We first created a new dataframe, named `funnel`, with only the columns we need: `avg_session_length_minutes`, `week_end_date`, and `energy_usage_flag`. Then, we simply create the steps by introducing conditions, as shown below:

</div>

```c++
funnel['base_week'] = 1
funnel['is_poor'] = funnel['energy_usage_flag'] == 'Poor'
funnel['is_below_time'] = funnel['avg_session_length_minutes'] < 5.5
```

These conditions are:

- Counting all the weeks.

- Only the weeks flagged with "Poor" energy efficiency.

- Within "Poor" flagged weeks, the ones that have an average session length of 5.5 mins.

***

<div align='center'>

Next, we create a new summary table, labeled `overall`, to contain our values for the funnel. This table will later be used to visualize our funnel analysis. The process for this summary table was simple, requiring only a few extra steps. This included:

</div>

<br>

- **Step Labels:** Renaming the steps with proper labels.

- **Step Conversion:** Dividing the current step count by the prvious step count.

- **Overall Conversion:** Dividing the current step count by the initial overall count.

<br>

<div align='center'>

| Step Name  | Count (Weeks) | Step Conversion (%) | Overall Conversion (%) |
|:----------------------------:|:--------:|:----------------:|:------------------:|
| Total Weeks                | 300    | NaN            | 100.0            |
| Poor Energy Efficiency     | 90     | 30.0           | 30.0             |
| Session Time < 5.5 mins    | 45     | 50.0           | 15.0             |

<br>

From this chart, we can immediately see that 50% of weeks for kiosk usage that are flagged with poor energy usage are sessions that are only ~5 mins or below. This is a key find, indicating that quick sessions actually result in higher normalized energy consumption than longer session times, as supported by this chart:

<br>

| Energy Efficiency Rating     | Average Session Time (Mins)     |
|:-------------:|:-----------:|
| Excellent   | 29.416000 |
| Fair        | 25.492222 |
| Good        | 26.743889 |
| Poor        | 5.192556  |

</div>

## 2. Visualizing The Funnel

This section details the methodology and findings from our funnel analysis, which was designed to identify and quantify the most ineffecient energy usages in the dataset based on key performance metrics. The visualization was created using the `plotly` library to generate an interactive funnel chart.


### Code Explanation

The Python script uses the `plotly.graph_objects` module to create a standard funnel chart.

1.  **Defining Funnel Data:** The script begins by defining a dictionary containing the three stages of our funnel and the pre-calculated number of weeks that fall into each stage. This data is then loaded into a pandas DataFrame.

2.  **Creating the Funnel Object:** The core of the visualization is the `go.Figure(go.Funnel(...))` command.
    * `y = df_funnel['step']`: This maps the names of our stages (e.g., "Total Weeks") to the Y-axis labels.
    * `x = df_funnel['count']`: This maps the numerical counts (300, 90, 45) to the width of each funnel section.
    * `textinfo = "value+percent initial"`: This is the most important parameter for understanding the labels on the chart.
        * `percent initial`: The percentage that the current step's count represents relative to the **very first (initial) step**. This is why the second step shows 30% (`90 / 300`) and the third step shows 15% (`45 / 300`).

3.  **Styling the Chart:** The remaining code in the `go.Funnel` call and the `fig.update_layout` section handles the visual styling, such as the colors of the bars, the connecting lines, the main title, and the fonts.

---

### Key Insights from the Funnel

The funnel visualization provides a clear, data-driven story about network performance, leading to a powerful, actionable insight.

* **Initial Filter (30% of Total):** The analysis starts with all 300 weeks in the dataset. The first filter immediately narrows this down, showing that **90 weeks (30% of the total)** qualify as having "Poor" energy efficiency. This establishes a significant baseline of underperformance.

* **The Critical Insight (15% of Total):** The most important finding comes from the next step. The funnel shows that of the original 300 weeks, only **45 (or 15%)** make it to the bottom stage. These are the weeks that not only have "Poor" efficiency but *also* have extremely low user engagement (average session time < 5.5 minutes).

* **The "So What" for the Stakeholder:** This analysis has successfully isolated the **45 absolute worst-performing weeks** in the dataset—the bottom 15%. The key takeaway is that the poorest network efficiency is strongly correlated with very low user engagement. This creates a clear directive for the operations team: investigate these specific 45 weeks to understand the root cause. This answers the critical question: **"Is low session time causing the poor efficiency, or is a poorly performing network causing users to disconnect quickly?"** Answering this question is the first step toward targeted operational improvements.

<br>

</div>
