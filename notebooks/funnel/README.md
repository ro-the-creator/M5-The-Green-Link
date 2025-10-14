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

From this chart, we can immediately see that 50% of weeks for kiosk usage that are flagged with poor energy usage are sessions that are only ~5 mins or below. This is a key find, indicating that quick session actually results in a higher normalized energy consumption than longer session times, as supported by this chart:

<br>

| Energy Efficiency Rating     | Average Session Time (Mins)     |
|:-------------:|:-----------:|
| Excellent   | 29.416000 |
| Fair        | 25.492222 |
| Good        | 26.743889 |
| Poor        | 5.192556  |

<br>

With an overall summary table now created, we are ready to move on to visualizing the funnel.

</div>