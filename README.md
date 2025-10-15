# Module 5: The Green Link

<div align='center'>

<img width="11520" height="4608" alt="M5-banner" src="https://github.com/user-attachments/assets/904aef7c-9b4f-4fd6-82bd-3f100a4ec0d8" />

### A data-driven analysis for CityBridge consortium, uncovering usage patterns and energy metrics with an aim to optimize kiosk availability, improve usage efficiency, and reduce energy waste.

</div>

<br>

# Project Overview

**[Stakeholder](#stakeholder)**  
 ↳ **[Business Problem](#business-problem)**  
  ↳ **[A Quick Look](#a-quick-look)**  
   ↳ **[Our Team](#our-team)**  
    ↳ **[Sources](#sources)**  
     ↳ **[Exploratory Data Analysis](#exploratory-data-analysis)**  
      🔹 [KPIs](#kpis)  
      🔹 [Feature Engineering](#feature-engineering)  
      🔹 [Funnel Analysis](#funnel-analysis)  
      🔹 [Cohort Analysis](#cohort-analysis)  
      🔹 [RFM/ROI](#rfmroi)  
     ↳ **[Ethics](#ethics)**  
    ↳ **[Repository Navigation](#repository-navigation)**

<div align='center'>

<br>

</div>

## Stakeholder

<div align='center'>

Based in New York City, **CityBridge** oversees and operates the LinkNYC program and its 5G expansion introduced in 2022. The consortium is a partnership between **Intersection**, a media technology firm, and **Boldyn Networks**, a company specializing in wireless infrastructure.

<br>

<img width="500" height="245" alt="IMG_1770" src="https://github.com/user-attachments/assets/d917b421-b7b9-4926-88a6-9789fa858d96" />

<br>
<br>

Since 2014, CityBridge has worked with the city to build what has become the world’s most extensive free public Wi-Fi network, designed to bring fast, reliable, and equitable internet access to communities throughout all five boroughs.

More information regarding CityBridge and their contributions to LinkNYC can be found [here](https://www.link.nyc/citybridge.html).

</div>

<br>

## Business Problem

<div align='center'>

Since its inception, LinkNYC has sought to close inequities amongst NYC communities by providing high-speed internet access at no cost to residents. To ensure this access is provided fairly and ethically, CityBridge has asked us to explore what's working and areas of improvement.

Our team had several factors that we wanted to explore, including kiosk availability in the five boroughs, usage patterns among residents, and energy consumption through bandwidth and upload/download data. Our aim was to provide an insightful report on key metrics that could aid consortium decisions and contributions.

Thus, we arrived to our overall question: 

**How can LinkNYC optimize kiosk availability and usage efficiency across boroughs while minimizing energy waste?**

</div>

## A Quick Look

<div align='center'>

<br>
<br>
<br>
<br>
<br>
  
(overall insights here)

<br>
<br>
<br>
<br>
<br>

</div>

<br>

## Our Team

<div align='center'>
    
![casual-septum](https://github.com/user-attachments/assets/86b1b472-797d-4c8e-ae70-3cf6ae68bc88)

### Rolando Mancilla-Rojas

Hi! I'm Rolando, but I mainly like to go by Ro. I have a particular interest in business/finance, and I enjoy getting my hands dirty in the data.

[LinkedIn](https://www.linkedin.com/in/rolandoma33/) | [GitHub](https://github.com/ro-the-creator)

</div>

<br>

<div align='center'>

![kabbo-headshot-fellow](https://github.com/user-attachments/assets/fbb3b205-bf95-449d-beba-144d5e2fefbc)

### Kabbo Sultan

My name is Kabbo Sultan, and I’m building my career at the intersection of data analytics and cybersecurity—helping businesses make smarter, safer decisions through data intelligence.

[LinkedIn](https://www.linkedin.com/in/kabbosultan/) | [GitHub](https://github.com/kabbosultan)

</div>

## Sources

<div align='center'>

We used data provided to us by CityBridge, which included LinkNYC's weekly usage and kiosk location data between the years of 2020 and (up-to-date) 2025.

</div>

<br>

- **[LinkNYC Weekly Usage Data](https://data.cityofnewyork.us/City-Government/LinkNYC-Weekly-Usage-Updated-/nxmt-wszr/about_data)** — From NYC OpenData

- **[LinkNYC Kiosk Location Data](https://data.cityofnewyork.us/Social-Services/LinkNYC-Kiosk-Locations/s4kf-3yrf/about_data)** — From NYC OpenData

## Insights
## Exploratory Data Analysis
### 1. Usage Trends & Patterns (Weekly Usage Data)

**Seasonality is a Major Factor:**
  Usage patterns show a clear seasonal trend. Wi-Fi sessions and unique clients consistently peak during the colder winter months (Jan–March) and reach their lowest points in April.
  This insight can help in planning maintenance schedules, avoiding high-traffic periods.

**Usage Quality is Stable:**
  We created a metric for "usage quality" by calculating the average Gigabytes (GB) transferred per session.
  The trend for this metric appears relatively stable over time, indicating consistent user behavior in terms of data consumption per connection.


### 2. Geographic Distribution & Availability (Kiosk Locations Data)

**Kiosk Distribution is Uneven:**
  The vast majority of LinkNYC kiosks are concentrated in Manhattan.
  Queens and Brooklyn have a moderate number, while the Bronx and Staten Island have very few.
  This highlights a potential *digital divide* and helps prioritize maintenance in high-density areas where a single outage has a larger impact.

**Network Availability is High:**
  Over **90%** of the kiosks in the dataset are listed with an `installation_status` of “Live,” meaning they are operational.
  This indicates a very high level of network uptime and provides a strong baseline to measure against when identifying faulty kiosks.

### KPIs

### Feature Engineering

### Funnel Analysis

### Cohort Analysis
**For the Stakeholder:**

Our comparative cohort analysis reveals a significant shift in the _pattern_ of user engagement since the 5G rollout in mid-2022. While overall engagement has remained stable, a new, predictable intra-month trend has emerged that presents a clear opportunity for operational and strategic optimization.

**The Core Insight:**

Our data consistently shows a dip in user engagement during the **second week of every month** in the post-5G era. While the first and fourth weeks remain periods of high engagement, this "Week 2 Slump" is a new, predictable pattern that we can leverage.

**Actionable Recommendations:**

We propose a two-pronged strategy to address this, depending on the immediate business goal:

1.  **For Operational Efficiency & Cost Savings:**
    *   **Action:** Designate the **second week of each month** as the primary window for scheduled network maintenance, software updates, and physical kiosk servicing.
    *   **Rationale:** By performing this necessary work during a predictable period of lower user activity, you minimize service disruption, reduce the risk of impacting users during peak engagement weeks (W1 and W4), and can potentially schedule maintenance crews more efficiently.
2.  **For Engagement Growth & Marketing:**
    *   **Action:** Target the **second week of each month** for specific user re-engagement campaigns.
    *   **Rationale:** Since we know engagement is likely to dip during this period, it is the ideal time to test promotions, display unique content on kiosk screens, or launch partnership offers with local businesses. This can help smooth out the monthly engagement curve and capture user attention during a time they are less active.
### RFM/ROI
**For the Stakeholder:**

Our comparative cohort analysis reveals a significant shift in the _pattern_ of user engagement since the 5G rollout in mid-2022. While overall engagement has remained stable, a new, predictable intra-month trend has emerged that presents a clear opportunity for operational and strategic optimization.

**The Core Insight:**

Our data consistently shows a dip in user engagement during the **second week of every month** in the post-5G era. While the first and fourth weeks remain periods of high engagement, this "Week 2 Slump" is a new, predictable pattern that we can leverage.

**Actionable Recommendations:**

We propose a two-pronged strategy to address this, depending on the immediate business goal:

1.  **For Operational Efficiency & Cost Savings:**
    *   **Action:** Designate the **second week of each month** as the primary window for scheduled network maintenance, software updates, and physical kiosk servicing.
    *   **Rationale:** By performing this necessary work during a predictable period of lower user activity, you minimize service disruption, reduce the risk of impacting users during peak engagement weeks (W1 and W4), and can potentially schedule maintenance crews more efficiently.
2.  **For Engagement Growth & Marketing:**
    *   **Action:** Target the **second week of each month** for specific user re-engagement campaigns.
    *   **Rationale:** Since we know engagement is likely to dip during this period, it is the ideal time to test promotions, display unique content on kiosk screens, or launch partnership offers with local businesses. This can help smooth out the monthly engagement curve and capture user attention during a time they are less active.

### **Part 2: Energy Efficiency Segmentation**

This analysis provides a strategic framework for network management by categorizing each week into one of four performance tiers based on a custom energy efficiency metric.


1.  **Visualization & ROI:** The code generates a summary table and a horizontal bar chart showing the total number of weeks in each performance segment. This is followed by a clear, actionable ROI strategy for each tier.

#### **Insights & Interpretation**

The bar chart shows the historical distribution of weekly performance. By design, the "Poor," "Fair," and "Good" categories contain an equal number of weeks (90 each), while the "Excellent" category contains the top-performing 30 weeks. This quantile method is a standard statistical approach for ranking and bucketing data into performance tiers.

**For the Stakeholder:** This segmentation provides a simple, data-driven calendar for operational planning:

*   **Excellent Weeks:** The goal is **replication**. These periods should be studied to understand what drives peak performance (e.g., city-wide events, specific user activities).
*   **Good Weeks:** The goal is **optimization**. These are strong weeks that could be pushed into the "Excellent" category with minor network tweaks.
*   **Fair/Poor Weeks:** The goal is **investigation and intervention**. These weeks should trigger an operational review to diagnose the cause of the inefficiency and schedule major, disruptive maintenance to minimize user impact.

### **Ethics & Equity Discussion**

As part of our analysis, we must consider the ethical implications of our findings. The kiosk\_locations dataset clearly shows that the vast majority of kiosks are in Manhattan. If we optimize 
maintenance and resources _only_ for the highest-yield areas, we risk reinforcing the digital divide and neglecting infrastructure in underserved boroughs like the Bronx and Staten Island.

## Recommendations
**Mitigation:** We recommend a dual maintenance strategy: a primary, data-driven plan for high-density areas, supplemented by a secondary, equity-focused plan that guarantees a baseline level of service and uptime for all kiosks, regardless of their current usage levels.

## Ethics


## Repository Navigation

- [data/](./data/)
- [notebooks/](./notebooks/)
  - [EDA/](./notebooks/EDA/)
  - [funnel/](./notebooks/funnel/)


> [!NOTE]
> This is a fictitious scenario created by the GitHub authors for academic purposes only.

