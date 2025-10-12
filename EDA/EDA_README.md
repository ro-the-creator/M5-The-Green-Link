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
