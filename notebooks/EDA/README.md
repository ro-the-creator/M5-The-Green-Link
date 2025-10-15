# Mod 5 Project: EDA & Data Cleaning

This document details the **Exploratory Data Analysis (EDA)** for the **LinkNYC project**.
The goal is to understand the structure, quality, and patterns within the two datasets provided.
The insights gathered here will form the foundation for defining **Key Performance Indicators (KPIs)**, feature engineering, and subsequent analysis.

---

## Business Context & Stakeholder

* **Stakeholder:** LinkNYC Consortium
* **Business Problem:** How can LinkNYC optimize kiosk availability and usage efficiency across boroughs while minimizing energy waste?

---

## Data Dictionaries

### 1. LinkNYC Weekly Usage

This dataset contains aggregated weekly metrics for the entire LinkNYC network.

| Column Name               | Description                                                                               |
| ------------------------- | ----------------------------------------------------------------------------------------- |
| `gb_per_session`          | A calculated metric for usage quality: `(tb_downloaded + tb_uploaded) * 1024 / sessions`. |
| `sessions`                | The total number of Wi-Fi sessions for the week.                                          |
| `avg_session_length`      | The average duration of a user session for the week.                                      |
| `unique_clients`          | The number of unique devices that connected during the week.                              |
| `tb_downloaded`           | The total volume of data downloaded in Terabytes (TB).                                    |
| `tb_uploaded`             | The total volume of data uploaded in Terabytes (TB).                                      |
| `cumulative_bandwidth_tb` | The running total of Terabytes transferred on the network up to the report date.          |
| `cumulative_sessions`     | The running total of all sessions on the network up to the report date.                   |
| `cumulative_subscribers`  | The running total of unique clients who have used the network to date.                    |
| `week_end_date`           | The week-ending date of the report, cleaned and converted for analysis.                   |

---

### 2. LinkNYC Kiosk Locations

This dataset provides geographic and status information for each individual kiosk.

| Column Name                          | Description                                                                 |
| ------------------------------------ | --------------------------------------------------------------------------- |
| `site_id`                            | A unique identifier for the kiosk site.                                     |
| `borough`                            | The NYC borough where the kiosk is located.                                 |
| `installation_status`                | The operational status of the kiosk (e.g., Live, Installed).                |
| `latitude`                           | The geographic latitude of the kiosk.                                       |
| `longitude`                          | The geographic longitude of the kiosk.                                      |
| `installation_complete`              | The date the physical installation was completed.                           |
| `activation_complete`                | The date the kiosk became operational ("Live").                             |
| `planned_kiosk_type`                 | The model or type of kiosk planned for the site (e.g., Link1.0, Link5G_Ad). |
| `ppt_id`                             | Permit Processing and Tracking System ID.                                   |
| `legacy_id`                          | A previous unique identifier for the kiosk.                                 |
| `council_district`                   | The NYC Council District where the kiosk is located.                        |
| `community_board`                    | The Community Board district where the kiosk is located.                    |
| `street_address`                     | The street address of the kiosk.                                            |
| `cross_street_1`                     | The first cross street of the kiosk's location.                             |
| `cross_street_2`                     | The second cross street of the kiosk's location.                            |
| `ixn_corner`                         | The corner of the intersection (e.g., NE, SW).                              |
| `postcode`                           | The postal code of the kiosk's location.                                    |
| `zoning`                             | The NYC zoning classification for the site.                                 |
| `neighborhood_tabulation_area_nat`   | The NYC zoning classification for the site.                                 |
| `building_identification_number_bin` | A unique ID for the building associated with the location.                  |
| `boroughblocklot_bbl`                | A unique tax lot identifier.                                                |
| `census_tract_ct`                    | The U.S. Census Tract for the location.                                     |
| `location`                           | A combined field with latitude and longitude.                               |

---

## EDA Questions

To address the business problem, our EDA will focus on answering the following questions:

### Usage Trends & Patterns (Weekly Usage Data)

* What are the overall trends in Wi-Fi sessions, unique users, and data (upload/download) over time?
* Is there evidence of seasonality in usage?
* What is the typical “quality” of a session (e.g., average data used per session)?
* Are there any data quality issues, such as missing weeks or extreme outliers?

### Geographic Distribution & Availability (Kiosk Locations Data)

* How are the LinkNYC kiosks distributed across the different boroughs?
* What percentage of the total kiosks are actually active and available for use?
* What are the key data quality issues to be aware of?

---

## Data Cleaning & Preparation

Before analysis, the following data preparation steps were performed:

* **Column Standardization:**
  All column names in both datasets were converted to a consistent `snake_case` format (e.g., `Site ID` → `site_id`) for easier coding.

* **Data Type Conversion:**

  * Date columns (`week_end_date`, `installation_complete`, `activation_complete`) were converted from text to proper datetime objects to enable time-based analysis.
  * The `avg_session_length` was converted to a numerical format (total seconds) to allow for calculations.

* **Null Value Assessment:**

  * An analysis of null values in the kiosk locations dataset was conducted. It revealed that core analytical columns like `borough` and `installation_status` are 100% complete.
  * Missing values were primarily found in secondary, non-essential columns (`ixn_corner`, `building_identification_number_bin`), confirming the high quality of the data for our specific business problem.
  * No rows needed to be dropped.

---

## At a Glance: EDA Answers

Based on the analysis and the generated plots, here are the key takeaways that directly address our initial EDA questions.

### 1. Usage Trends & Patterns (Weekly Usage Data)

* **Seasonality is a Major Factor:**
  Usage patterns show a clear seasonal trend. Wi-Fi sessions and unique clients consistently peak during the colder winter months (Jan–March) and reach their lowest points in April.
  This insight can help in planning maintenance schedules, avoiding high-traffic periods.

* **Usage Quality is Stable:**
  We created a metric for "usage quality" by calculating the average Gigabytes (GB) transferred per session.
  The trend for this metric appears relatively stable over time, indicating consistent user behavior in terms of data consumption per connection.

---

### 2. Geographic Distribution & Availability (Kiosk Locations Data)

* **Kiosk Distribution is Uneven:**
  The vast majority of LinkNYC kiosks are concentrated in Manhattan.
  Queens and Brooklyn have a moderate number, while the Bronx and Staten Island have very few.
  This highlights a potential *digital divide* and helps prioritize maintenance in high-density areas where a single outage has a larger impact.

* **Network Availability is High:**
  Over **90%** of the kiosks in the dataset are listed with an `installation_status` of “Live,” meaning they are operational.
  This indicates a very high level of network uptime and provides a strong baseline to measure against when identifying faulty kiosks.

---

## Feature Engineering / KPIs

After initial EDA, we were able to explore deep within the dataset to uncover more trends and concerns, especially regarding kiosk usage and energy consumption.


### 1. Calculations

- **Activation Time:** Used timedelta to find the difference between `installation_complete` and `activation_complete`. We can sort this new column by days to find possible problematic kiosks.

- **Kiosk Age:** Used timedelta again, this time to find the difference between `activation_complete` and today's date. Sorting this new column will help us find the longest running kiosks, which may be due for maintenance/repair.

- **Weekly Session Change (&):** used `.diff()` and `.shift(1)` create the variables needed for a weekly change. This can be used as a KPI to find weeks of the highest/lowest change in sessions.

- **Average Session Time per Week:** Required the use of `pd.to_datetime()` to first convert the object column of `avg_session_length`. Then, `.dt.hour`, `.minute`, and `.second` was all added together (with conversion calculations) to get a create a new column, `avg_session_length_seconds`. 

- **Energy Efficiency:** This metric require a deeper understanding of our data. Since we lacked any energy metric, we had to create an energy proxy.

This will look like:

<div align='center'>

Energy Efficiency = Data Usage / Energy Consumption Proxy

Where...

Data Usage (GB) = (TB Uploaded + TB Downloaded) * 1024

AND

Energy Consumption Proxy = (Sessions * 0.85) + (Unique Clients * 0.15)

**Afterwards, we normalize this by dividing Energy Efficiency over the total growing Bandwidth, converted into megabytes (MB)**

</div>

**NOTES**

- we multiply by 1024 to transform from TB to GB.

- Data Usage is by week, since that is what our dataset is already aggregated by.

- We add sessions by unique clients for an approximation of energy consumption. They represent our user activity load.
    
    - While unique clients may already be represented within, we will add both to try and approximate the higher end of our user activity load.

    - For better fairness, we weigh the factors of our energy consumption proxy by only taking into account a determined percentage of them (thus, 90% of total sessions and 10% of unique users).

***

<br>

# At a Glance: Feature Engineering / KPIs Answers

## KPIs

### 1. Average Activation Time
  - **Business Goal:** To measure and optimize the efficiency of the kiosk deployment process, from physical installation to live operation.
  - **Justification:** A long activation time can signal significant bottlenecks in the deployment pipeline, such as infrastructure challenges, permitting delays, or technical issues. By tracking the average activation time, the operations team can establish a baseline, identify outliers, and investigate the root causes of delays. This KPI is crucial for streamlining the rollout of new kiosks and improving the speed to market.

- **Implementation Logic:**
  - **Data Source:** kiosk_locations dataset.
  - **Calculation:** For each kiosk, calculate Activation Time = avg.activation_complete - avg.installation_complete.


- **KPI:** The average of the Activation Time across all "Live" kiosks. This can be further segmented by borough or planned_kiosk_type to identify specific problem areas.

<div align='center'>

### Average Time From Kiosk Installation to Activation: 170 days 15:40:55.790363482

</div>

### 2. Average Kiosk Age
- **Business Goal:** To inform a proactive maintenance and hardware refresh strategy.
- **Justification:** As kiosks age, they become more susceptible to hardware failure and may be running on older, less efficient technology. Tracking the average age of the "Live" kiosks in the network allows the maintenance team to forecast potential issues and prioritize inspections or upgrades for the oldest units. This shifts the team from a reactive to a proactive maintenance model, minimizing downtime and ensuring a consistent user experience.

- **Implementation Logic:**
  - **Data Source:** kiosk_locations dataset.
  - **Calculation:** For each "Live" kiosk, calculate Kiosk Age = Current Date - activation_complete.

- **KPI:** The average of the Kiosk Age across all "Live" kiosks. This metric should be monitored over time to understand the overall aging of the network's infrastructure.

<div align='center'>

### Average Age of Kiosks: 17804 days 16:29:53.859173120

</div>

### 3. Network Energy Efficiency
- **Business Goal:** To create a standardized metric for monitoring the network's efficiency by modeling a proxy for energy consumption.
- **Justification:** Direct energy consumption data is unavailable. To address this, we've developed a proxy that models energy usage based on user activity load (sessions and unique clients). By comparing the data delivered (value) to the modeled energy consumed (cost proxy), we can create a powerful efficiency score. Tracking this KPI is essential for financial forecasting, promoting sustainability, and making data-driven decisions about hardware deployment.
- **Implementation Logic:**
  - **Data Source:** weekly_usage dataset.
  - **Calculation (Multi-step):**
    - **Calculate Data Usage (GB):** (tb_downloaded + tb_uploaded) * 1024
    - **Calculate Energy Consumption Proxy:** (sessions * 0.85) + (unique_clients * 0.15)
    - **Calculate Initial Efficiency Score:** Data Usage (GB) / Energy Consumption Proxy
    - **Normalize the Score:** Divide the Initial Efficiency Score by the cumulative_bandwidth_tb (converted to MB) to get a final KPI that accounts for network growth.

- **KPI:** Dimensionless data transfer per session. Higher is good.

<div align='center'>

### Average Energy Efficiency: 0.032958

</div>

  <br>

## Feature Engineering

Our feature engineering included a variety of views into the data. Some of them also spawned KPIs, though they are generally well used throughout the analysis of the project.

### 1. Activation Time

This is a metric that can be used by the deployment team, as well as the higher ups. It gives a view of kiosks that took a long time to activate after installation, which can point to issues with infrastructure, permitting, technical issues, etc. Using this feature, the team can flag problematic kiosks and get further insight as to factors that contribute to long kiosk activation times.

### 2. Kiosk Age

This metric can be useful for finding the oldest running kiosks, which can be used by the maintenance team to prioritize which kiosks need attention the most. Going forward, a new column can also be created that would mark the latest maintenence date.

### 3. Weekly Session Change (%)

This metric will be useful for doing a weekly track of session changes, and can be supported by other data sources to find factors contributing to session changes. It checks the difference in percentage of the amount of sessions each week, positive or negative changes.

### 4. Average Session Time (Mins)

This can help support our weekly session change column, by showing the actually length of average session usage per week. I also included an overall calculation, to show how much LinkNYC's usage has increased since its inception. Since our data is already aggregated by week, this was a simply feature to add, but effective in its use.

### 5. Energy Efficiency

This is our key metric we want. This will help CityBridge note their energy consumption and how efficient their kiosks are really running. However, given we lack energy usage data, we will have to create an energy consumption proxy using TB uploaded/downloaded, # of sessions, and # of unique clients.

### 6. Energy Efficiency Rating Flag

This column detects excellent, good, fair, or poor energy efficient usage weeks. This metric was calculated based on percentile thresholds, namely:

- **Excellent:** Top 10%

- **Good:** 60% - 90%

- **Fair:** 30% - 60%

- **Poor:** Bottom 30%