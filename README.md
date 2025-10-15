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

***

### KPIs

#### 1. Average Activation Time

A long activation time can signal significant bottlenecks in the deployment pipeline, such as infrastructure challenges, permitting delays, or technical issues. By tracking the average activation time, the operations team can establish a baseline, identify outliers, and investigate the root causes of delays. This KPI is crucial for streamlining the rollout of new kiosks and improving the speed to market.

<div align='center'>

**Business Goal:** To measure and optimize the efficiency of the kiosk deployment process, from physical installation to live operation.

</div>

<br>

#### 2. Average Kiosk Age

As kiosks age, they become more susceptible to hardware failure and may be running on older, less efficient technology. Tracking the average age of the "Live" kiosks in the network allows the maintenance team to forecast potential issues and prioritize inspections or upgrades for the oldest units. This shifts the team from a reactive to a proactive maintenance model, minimizing downtime and ensuring a consistent user experience.

<div align='center'>

**Business Goal:** To inform a proactive maintenance and hardware refresh strategy.

</div>

<br>

#### 3. Network Energy Efficiency

Direct energy consumption data is unavailable. To address this, we've developed a proxy that models energy usage based on user activity load (sessions and unique clients). By comparing the data delivered (value) to the modeled energy consumed (cost proxy), we can create a powerful efficiency score. Tracking this KPI is essential for financial forecasting, promoting sustainability, and making data-driven decisions about hardware deployment.

<div align='center'>

**Business Goal:** To create a standardized metric for monitoring the network's efficiency by modeling a proxy for energy consumption.

</div>
<br>

***

### Feature Engineering



### Funnel Analysis

<div align='center'>

#### Funnel Conversion Flow

Weekly Usage → Weeks marked “Poor” Energy Efficiency → Average Session < 5.5 mins

<br>

#### Visualization

<br>

</div>

<div align='center'>

<img width="1328" height="450" alt="newplot" src="https://github.com/user-attachments/assets/c5890bf9-bf7e-4506-9171-4991d1467ebe" />

<br>

Here, we start with 300 weeks: the makeup of our weekly usage dataset. As we go down the steps, we can see that we are left with 45 weeks that are marked "Poor" energy efficiency _AND_ average session < 5.5 mins. More significantly, the makeup of short average session times in the "Poor" category is 50%.

</div>

<div align='center'>

#### Conversion of Interest

Our conversion of interest was the drop-off of weeks marked “Poor” efficiency to those with average sessions being less than 5.5 minutes (rather, the number of poor weeks that remained). This was an important conversion for us to show that quick average sessions are actually contributing to higher energy consumption, which is reflected by their poor energy efficiency ratings. 

</div>

<div align='center'>

#### Real-World Example

Imagine you are a tourist visiting NYC, and need to connect to the internet in order to call an Uber ride. You don’t speak much English, but luckily, you find a kiosk that can translate into your language. You load up the kiosk, connect to the wifi, and call an Uber. Within 5 minutes, you have already left the kiosk and are on your way back to the hotel.

Scenarios like these are undoubtedly common in Manhattan, the most tourist-heavy borough with the highest number of LinkNYC kiosks. It is scenarios like these that are contributing to the highest energy consumption costs across the grid. 

NYC is the fastest city on Earth. Fast kiosk transactions aren’t just expected; they’re inevitable. The energy consumption of these fast transactions is too high a cost to continue operating this way.

</div>

***

### Cohort Analysis

<div align='center'>

#### Pre-5G

<img width="740" height="568" alt="pre-5G" src="https://github.com/user-attachments/assets/f9c06a4c-3fb4-42ba-853e-4cd0de4671d0" />



#### Post-5G

<img width="740" height="722" alt="post-5G" src="https://github.com/user-attachments/assets/fbc16e36-5267-4fc2-bb3c-8767ec22771b" />


</div>

<br>

Our comparative cohort analysis reveals a significant shift in the _pattern_ of user engagement since the 5G rollout in mid-2022. While overall engagement has remained stable, a new, predictable intra-month trend has emerged that presents a clear opportunity for operational and strategic optimization.

**The Core Insight:**

Our data consistently shows a dip in user engagement during the **second week of every month** in the post-5G era. While the first and fourth weeks remain periods of high engagement, this "Week 2 Slump" is a new, predictable pattern that we can leverage.

***

### RFM/ROI

<div align='center'>

#### Visualization

<br>

<img width="989" height="590" alt="RFM" src="https://github.com/user-attachments/assets/16f084f4-5251-4fa6-869e-4a495b25dcef" />

<br>

Our comparative cohort analysis reveals a significant shift in the _pattern_ of user engagement since the 5G rollout in mid-2022. While overall engagement has remained stable, a new, predictable intra-month trend has emerged that presents a clear opportunity for operational and strategic optimization.

</div>

<div align='center'>

**The Core Insight:**

Our data consistently shows a dip in user engagement during the **second week of every month** in the post-5G era. While the first and fourth weeks remain periods of high engagement, this "Week 2 Slump" is a new, predictable pattern that we can leverage.

</div>

<br>

***

## Recommendations

### **Funnel Results:**

Our funnel analysis showed a significant figure: that 50% of "Poor" energy efficiency weeks have short average session times. As a result, we recommend:

1. **Reconfiguring System Hardware:**
    - **Action:** Dedicate the Maintenance & Deployment teams to (re)configure the kiosks. Set kiosks to sleep during off-use rather than completely shutting down.
    - **Rationale:** A likely cause of this issue may be that the operating system is constantly turning on and shutting off, using significant power in doing so. Setting the OS to sleep will actually use less energy since it will conserve the computer's current state, rather than fulling starting up everything upon powering on. The system can also be set to fully shut down during the least used hours, for even more optimized energy conservation.
2. **Time-Based Sessions:**
    - **Action:** Implementing a new feature that allows users to select their session time.
    - **Rationale:** Allowing users to select pre-slotted session times will allow for easier configuration and energy conservation. This recommendation will not only make it easier to track short session times but also allow for the deployment of a future solution for short average session times.

### **Cohort Results:**

We propose a two-pronged strategy to address this, depending on the immediate business goal:

1.  **For Operational Efficiency & Cost Savings:**
    *   **Action:** Designate the **second week of each month** as the primary window for scheduled network maintenance, software updates, and physical kiosk servicing.
    *   **Rationale:** By performing this necessary work during a predictable period of lower user activity, you minimize service disruption, reduce the risk of impacting users during peak engagement weeks (W1 and W4), and can potentially schedule maintenance crews more efficiently.
2.  **For Engagement Growth & Marketing:**
    *   **Action:** Target the **second week of each month** for specific user re-engagement campaigns.
    *   **Rationale:** Since we know engagement is likely to dip during this period, it is the ideal time to test promotions, display unique content on kiosk screens, or launch partnership offers with local businesses. This can help smooth out the monthly engagement curve and capture user attention during a time they are less active.

**Mitigation:** We recommend a dual maintenance strategy: a primary, data-driven plan for high-density areas, supplemented by a secondary, equity-focused plan that guarantees a baseline level of service and uptime for all kiosks, regardless of their current usage levels.

### RFM / ROI Results:

This segmentation provides a simple, data-driven calendar for operational planning:

1. **Action:** Track Flagging System for Targets:
    - **Excellent Weeks:** The goal is **replication**. These periods should be studied to understand what drives peak performance (e.g., city-wide events, specific user activities).
    -   **Good Weeks:** The goal is **optimization**. These are strong weeks that could be pushed into the "Excellent" category with minor network tweaks.
    -   **Fair/Poor Weeks:** The goal is **investigation and intervention**. These weeks should trigger an operational review to diagnose the cause of the inefficiency and schedule major, disruptive maintenance to minimize user impact.

## Ethics

In considering our ethical commitments when analyzing data, we were immediately drawn to the idea of energy consumption. There are over 2000 kiosks available across NYC, and they all draw from the power grid. With an increased concern of energy consumption due to AI datacenters, we wanted to minimize energy consumption in any other aspects.

As part of our analysis, we also must consider the ethical implications of our findings. The kiosk\_locations dataset clearly shows that the vast majority of kiosks are in Manhattan. If we optimize maintenance and resources _only_ for the highest-yield areas, we risk reinforcing the digital divide and neglecting infrastructure in underserved boroughs like the Bronx and Staten Island.

## Repository Navigation

- [data/](./data/)
- [notebooks/](./notebooks/)
  - [EDA/](./notebooks/EDA/)
  - [funnel/](./notebooks/funnel/)


> [!NOTE]
> This is a fictitious scenario created by the GitHub authors for academic purposes only.

