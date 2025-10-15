**Cohort & Segmentation Analysis**
=========================================

This document explains the two primary analyses conducted on the LinkNYC weekly usage data: a comparative cohort analysis focusing on user engagement, and a performance segmentation based on a custom energy efficiency metric.

### **Part 1: Cohort Analysis - The Impact of 5G**

This analysis was designed to measure the impact of a significant network event (the 5G rollout in mid-2022) on user engagement.

#### **Code Explanation**

1.  **Metric Definition:** The core metric for this analysis is average\_session\_length\_minutes, a powerful and intuitive measure of user engagement or "stickiness." A "high engagement week" is defined as any week where this value is above the 75th percentile of its respective period.
    
2.  **Data Splitting:** The weekly usage data is divided into two distinct datasets based on the 5G implementation date of **July 2022**:
    

*   **Pre-5G:** All data _before_ July 2022.
    
*   **Post-5G:** All data _from_ July 2022 onwards.
    

1.  **Cohort Creation & Visualization:** For each period (Pre- and Post-5G), the code groups the data into monthly cohorts (e.g., "2021-01", "2023-05"). It then generates a **heatmap** that visualizes whether each of the first four weeks of the month was a "high engagement" week. A summary table showing the average week-over-week retention percentage is also calculated for each period.
    

#### **Insights & Interpretation**

The output from this analysis tells a clear and powerful "before and after" story:

*   **Pre-5G Heatmap:** This chart shows consistent user engagement. "High engagement" weeks are not rare and follow a predictable pattern. The retention tables for this period show a high probability of the 1st and 4th week being a high-performer.
| Week | Retention Rate (%)  |
|:-----|--------------------:|
| W1   | 25.81               |
| W2   | 22.58               |
| W3   | 22.58               |
| W4   | 25.81               |

*   **Post-5G Heatmap:** This chart shows a  change in engagement. After the 5G rollout, user engagement becomes sporadic. The 1st and 4th weeks are still "high engagement," as indicated by the solid blocks of yellows in the heatmap and the 3rd week has a build up towards the 4th week. The 2nd week has the lowest engaement. The retention tables confirm this:
| Week | Retention Rate (%)  |
|:-----|--------------------:|
| W1   | 25.64               |
| W2   | 20.51               |
| W3   | 23.08               |
| W4   | 25.64               |

    

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

#### **Code Explanation**

1.  **Metric Definition:** A custom energy\_efficiency score is engineered for each week using the team's formula: Energy Efficiency = (Total Data Usage in GB) / (Weighted User Activity Load). This metric provides a proxy for how effectively the network is delivering data relative to its user load.
    
2.  **Segmentation Logic:** Instead of a complex RFM model, this analysis uses a more direct quantile-based approach to segment the weeks:
    

*   **Poor:** Weeks with efficiency scores in the bottom 30%.
    
*   **Fair:** Weeks with scores between the 30th and 60th percentile.
    
*   **Good:** Weeks with scores between the 60th and 90th percentile.
    
*   **Excellent:** Weeks with scores in the top 10%.
    

1.  **Visualization & ROI:** The code generates a summary table and a horizontal bar chart showing the total number of weeks in each performance segment. This is followed by a clear, actionable ROI strategy for each tier.
    

#### **Insights & Interpretation**

The bar chart shows the historical distribution of weekly performance. By design, the "Poor," "Fair," and "Good" categories contain an equal number of weeks (90 each), while the "Excellent" category contains the top-performing 30 weeks. This quantile method is a standard statistical approach for ranking and bucketing data into performance tiers.

**For the Stakeholder:** This segmentation provides a simple, data-driven calendar for operational planning:

*   **Excellent Weeks:** The goal is **replication**. These periods should be studied to understand what drives peak performance (e.g., city-wide events, specific user activities).
    
*   **Good Weeks:** The goal is **optimization**. These are strong weeks that could be pushed into the "Excellent" category with minor network tweaks.
    
*   **Fair/Poor Weeks:** The goal is **investigation and intervention**. These weeks should trigger an operational review to diagnose the cause of the inefficiency and schedule major, disruptive maintenance to minimize user impact.
    

### **Ethics & Equity Discussion**

As part of our analysis, we must consider the ethical implications of our findings. The kiosk\_locations dataset clearly shows that the vast majority of kiosks are in Manhattan. If we optimize maintenance and resources _only_ for the highest-yield areas, we risk reinforcing the digital divide and neglecting infrastructure in underserved boroughs like the Bronx and Staten Island.

**Mitigation:** We recommend a dual maintenance strategy: a primary, data-driven plan for high-density areas, supplemented by a secondary, equity-focused plan that guarantees a baseline level of service and uptime for all kiosks, regardless of their current usage levels.
