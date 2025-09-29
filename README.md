# Investigating Money Laundering Activity with Advanced Data Wrangling

## Overview

This project presents a case study I completed in six hours for a late-stage interview for a Lead Data Scientist position at a late stage startup. The problem statement focused on conducting in-depth data analysis on a **12K-observation** dataset of money transfer records at a flowershop business based in California in order to uncover potentially suspicious signs of money laundering activity, that could support possible law enforcement action. The dataset provided variables covering transaction size, frequency, and geographic destinations, enabling in-depth analysis of anomalous transaction patterns. You can check out the final report in the "Final Report.pdf" file included in this repo.

## Executive Summary

The dataset reveals a strong skew toward small-value transfers, with notable clustering just below common FinCEN reporting regulatory thresholds (**$2.5–3K** and **$7–8K**). As we uncovered that several workers showed patterns of unusually high transaction volumes and amounts, we selected three of these workers (#6, 11, and 39) for a deeper investigation of their transfer patterns in the second part of the case study. Our final recommendation was to prioritize workers 11 and 39 for immediate review of what we consider highly suspicious money laundering activity, with Worker 6 marked as lower risk but still requiring law enforcement follow-up.

## Data Exploration

### A. Transaction Size

![Transaction Size](images/viz1.png)
**Takeaway:** Most transfers fall below $1,000, with a smaller but notable set clustering just under $3,000. This aligns with regulatory record-keeping thresholds and indicates possible "layering" activity, whereby pay agents may be sending multiple transactions right under the threshold to stay under reporting limits.

![Transaction Size](images/viz2.png)
![Transaction Size](images/viz3.png)
**Takeaway:** Zooming into the $3–10K range shows few transfers above the $5,000 threshold, but interestingly repeated transactions near the **$8,000 mark**. This pattern may be consistent with efforts to avoid triggering FinCEN's mandatory Currency Transaction reports for amounts above $10K, and should be further investigated later in our analysis.

### B. Transaction Frequency

![Transaction Frequency](images/viz4.png)
![Transaction Frequency](images/viz5.png)
**Takeaway:** Send transactions peaked in 2016–17, before gradually declining through 2020. Daily activity shows two peaks—midday and early evening—indicating behavior tied to work and leisure hours.

![Transaction Frequency](images/viz6.png)
![Transaction Frequency](images/viz7.png)
![Transaction Frequency](images/viz8.png)
**Takeaway:** Pay transactions follow a similar trajectory, peaking in 2017 and then declining steadily. Counts remain evenly distributed across days of the month but show a gradual mid-to-late month decline. Looking at time of day, we can also observe a pattern of payouts peaking between **2–5 p.m**.

### C. Highest Transaction Frequency Workers

![Send and Pay Agents](images/viz9.png)
**Takeaway:** Agents 11 and 39 here appear suspicious here due to their unusually high transactions counts and amounts, warranting further review. 

![Send and Pay Agents](images/viz10.png)
**Takeaway:** Agents 11, 39 and 73 look suspicious here given their unusually high transactions counts and amounts. Agent 6 also appears to have unusually large total transaction amounts on a relatively large number of transactions (153), which should also be cause for review. 

![Send and Pay Agents](images/viz11.png)
**Takeaway:** agent_635 and agent_515 both appear suspicious with average and median transaction amounts clustering around the $8K mark, which might be a strong signal of money laundering activity given this is a common transaction amount to fly under the radar of AML authorities. Pending further review, the four agents after these two should also likely be further investigated given their >$5K pay amounts.

![Send and Pay Agents](images/viz12.png)
**Takeaway:** The top six agents shown in these graphs with average and median transaction amounts of **$2,500** appear suspicious given these amounts might be chosen purposefully to be right under FinCEN's first $3K transaction limit. Given these suspicious amounts, these six appear to be good candidates for further investigation.

### D. Send and Pay Locations

![Send and Pay Locations](images/viz13.png)
**Takeaway:** From these graphs we can see that the US is by far the country with the highest transaction counts and amounts, with Guatemala coming second after this. Interestingly for Pay Agent countries, Mexico and El Salvador rank as the two largest destinations, followed by the US, Guatemala and Tonga. 

As we will see in the next graph that California is the largest Send agent state in the dataset, we hypothesize that these patterns might correlate with California’s significant Latino population which may be sending remittances to family and friends in those Latin American countries. However further research and exploration is needed to confirm this. 


![Send and Pay Locations](images/viz14.png)
**Takeaway:** From these graphs we can see that CA is by far the state with the highest total counts and amounts of transactions, with Minnesota a distant second after this. Interestingly for Pay Agent states, these rank as California, Michoacán and Jalisco in Mexico, and Minnesota for both highest total counts and amounts of transactions. 

## Hypotheses

1. Frequent transactions by the same sender within 72 hours may indicate layering to disguise illicit fund origins.
2. Transfers occurring late at night or outside typical business hours may reflect deliberate evasion of scrutiny.
3. Actors with unusually high transaction volumes compared to peers may be linked to laundering networks.
4. Transactions clustering just below $3K or $10K thresholds likely suggest efforts to avoid reporting requirements.

## Investigations of Key Pay Agents

### Pay Agent 6

![Pay Agent 6](images/viz15.png)
![Pay Agent 6](images/viz16.png)
![Pay Agent 6](images/viz17.png)
![Pay Agent 6](images/viz18.png)
![Pay Agent 6](images/viz19.png)
- While we previously observed Pay agent 6 had an above-normal transaction frequency that was deemed suspicious, we can observe that none of their transactions fall outside of normal business hours, and we see only a low number of “layering” transaction clusters overall with there being only four in total between 2016 and 2019.
- We can also observe that all payments originated from the United States with Tonga being the only receiver country, suggesting a limited geographic scope rather than a broader network of transfers.
- Although some of the 15 transactions in the $2K range and the five transactions near the $3K mark may look suspicious, we can observe no transactions above $5K , which makes the overall pattern appear less consistent with laundering activity.
- Given these factors, although it would still be prudent for California law enforcement to review sending activity and conduct further checks, the evidence seems to suggest a lower risk of money laundering.


### Pay Agent 11

![Pay Agent 11](images/viz20.png)
![Pay Agent 11](images/viz21.png)
![Pay Agent 11](images/viz22.png)
![Pay Agent 11](images/viz23.png)
![Pay Agent 11](images/viz24.png)

- As we noted previously, a high frequency of transactions for pay agent 11 already seems suspicious at the outset.
- We can further note that a non-negligible share of these transactions fall outside of normal business hours, about 10% of the total, which strengthens the concern of unusual activity.
- We can also observe a large number of layering spikes spread across the full time period, with more than ten instances of 72h windows registering more than three transactions, and notably six instances of four or more in that same time window, which is highly suspicious.
- In addition, we see a significant volume of transactions directed to Guatemala, Mexico, and El Salvador, destinations that are often cited in connection with gang or criminal networks involved in money laundering.
- Taken together, these patterns make Pay Agent 11 the case with the highest level of suspicion, and we strongly recommend that this agent be investigated further by California law enforcement.


### Pay Agent 39

![Pay Agent 39](images/viz25.png)
![Pay Agent 39](images/viz26.png)
![Pay Agent 39](images/viz27.png)
![Pay Agent 39](images/viz28.png)
![Pay Agent 39](images/viz29.png)
- The high transaction count that we had noted previously was a cause for concern for this agent as well.
- We can observe a relatively low number of transactions above the $5,000 mark with only five total, and that most transactions fall under **$3,000**.
- However, it seems that there might be some layering behavior present given we can observe ~15 cases of 72-hour periods with more than two transactions, which may be evidence of layering behavior, like that observed with agent 11.
- Additionally, about 15% of the total transactions occur after 8 p.m., which may also be considered suspicious, as most legitimate transactions tend to occur during standard business hours.
- Given the presence of potential layering activity and the notable share of after-hours transactions, we recommend that Pay Agent 39 be investigated further for possible money laundering activity.

## Final Recommendations

We recommend prioritizing investigations into Pay Agents 11 and 39, both of which demonstrate repeated layering and suspicious after-hours activity. Pay Agent 11 poses the highest concern due to both transaction volume and foreign payout destinations linked to laundering networks. Pay Agent 6, though less suspicious, should still be reviewed due to its transaction frequency and clustering below thresholds. 

![Final recommendations](images/viz30.png)

Beyond the three agents that displayed high frequency counts, we also recommend investigating some of the agents with very low average time deltas between send and pay operations, which are shown here for the top 15. This pattern can be another marker of potential money laundering activity, as short gaps between sending and receiving wires may indicate that both the send and pay agents were notified ahead of time, allowing for immediate payout once the transfer was initiated.