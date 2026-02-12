# Statistical Process Control with Western Electric Rules

## Introduction

Statistical Process Control (SPC) is a methodical approach used to monitor and control processes through the application of statistical methods. This system uses **XmR Charts** (Individuals and Moving Range Charts) combined with **Western Electric Rules** to detect unusual patterns in your metrics.

At Soundtrack, we use SPC to monitor key business metrics like subscription zones, identifying when metrics show unusual behavior that requires investigation.

---

## What Are XmR Charts?

An **XmR chart** consists of two components:

- **X Chart (Individuals Chart):** Plots individual metric values over time
- **mR Chart (Moving Range Chart):** Plots the volatility between consecutive measurements

### Key Components

- **Center Line (X̄):** The mean (average) of your metric
- **Control Limits (UCL/LCL):** Boundaries set at ±3σ (standard deviations) from the mean
- **Zone Lines:** Intermediate boundaries at ±1.5σ and ±2σ
- **Moving Range:** The absolute difference between consecutive values

---

## The Western Electric Rules

The Western Electric Rules are a set of decision rules for detecting unusual patterns in control charts. Our system uses **5 primary rules** to identify when metrics are showing non-random behavior.

### Rule 1: Beyond 3σ (Critical)

**🚨 Severity: Critical**

**What it detects:** A single point falls outside the 3σ control limits (UCL/LCL)

**What it means:** An extreme, unprecedented value that's statistically very unlikely to occur by chance alone (99.7% of normal variation should be within 3σ)

**Business explanation:** Something exceptional happened - either a major success, a significant problem, or potentially a data quality issue

**When to investigate:**

- Check if there was a known event (product launch, outage, campaign)
- Verify data quality and measurement accuracy
- If legitimate, determine if this is a one-time event or new pattern

**Example:** Your "New Sound Zones" metric suddenly jumps from 150 to 450 in one day

---

### Rule 2: 2 of 3 Beyond 2σ (High)

**⚠️ Severity: High**

**What it detects:** 2 out of 3 consecutive points fall beyond 2σ on the same side of the mean

**What it means:** Unusual clustering near the warning limits - not quite extreme enough to trigger Rule 1, but showing a pattern that's unlikely to be random

**Business explanation:** The process is showing early signs of a shift or unusual behavior

**When to investigate:**

- Look for recent changes in the business (pricing, features, competition)
- Check if there's a developing trend
- Monitor closely over the next few data points

**Example:** Daily churned zones show 2 days out of 3 with unusually high churn (both above the 2σ line)

---

### Rule 3: 4 of 5 Beyond 1σ (Medium)

**⚠️ Severity: Medium**

**What it detects:** 4 out of 5 consecutive points fall beyond 1σ on the same side of the mean

**What it means:** A subtle but persistent shift pattern - the metric is consistently running higher or lower than average

**Business explanation:** The process mean may have shifted slightly, or there's sustained pressure in one direction

**When to investigate:**

- Review for gradual changes in business conditions
- Check for seasonal patterns or calendar effects
- Consider if this represents a new "normal" level

**Example:** New subscriptions are consistently above average for 4 out of 5 days (though not dramatically high)

---

### Rule 4: 8 Consecutive Same Side (High)

**⚠️ Severity: High**

**What it detects:** 8 or more consecutive points fall on the same side of the center line

**What it means:** A sustained shift in the process level - the mean has likely changed

**Business explanation:** Your metric's baseline has shifted. This could be positive (sustained growth) or negative (sustained decline)

**When to investigate:**

- Identify what changed around the time the shift began
- Determine if this is temporary or permanent
- Consider updating control limits if the new level is sustainable

**Example:** Resubscribed zones are consistently above average for 8 straight days, suggesting a successful win-back campaign

---

### Rule 5: 6 Consecutive Trending (Medium)

**⚠️ Severity: Medium**

**What it detects:** 6 consecutive points trending in the same direction (either all increasing or all decreasing)

**What it means:** A consistent directional trend - the metric is steadily moving up or down

**Business explanation:** There's momentum in one direction that may indicate gradual process change, growth, or decline

**When to investigate:**

- Determine if the trend is expected or concerning
- Project where the trend is heading
- Decide if intervention is needed to maintain or reverse the trend

**Example:** Churned zones increase slightly each day for 6 consecutive days, indicating mounting churn pressure

---

### Moving Range (MR) Violations (High)

**⚠️ Severity: High**

**What it detects:** The Moving Range (difference between consecutive values) exceeds its Upper Control Limit

**What it means:** Unusual volatility - the metric changed dramatically from one period to the next

**Business explanation:** Something caused a sudden jump or drop in your metric

**When to investigate:**

- Check for data quality issues (missing data, double-counting, etc.)
- Look for known events causing volatility
- If legitimate, understand what drove the sudden change

**Example:** New zones went from 150 to 320 in one day (a jump of 170), indicating unusual volatility

---

## How to Use These Rules

### 1. **Prioritize by Severity**

- **Critical (Rule 1, MR Violations):** Investigate immediately
- **High (Rule 2, Rule 4):** Review within 24 hours
- **Medium (Rule 3, Rule 5):** Monitor and investigate if pattern continues

### 2. **Look for Multiple Rules Triggered**

When multiple rules fire on the same data points, it strengthens the signal that something unusual is happening.

### 3. **Context Matters**

Always interpret signals in business context:

- Is this expected (product launch, holiday season)?
- Is this concerning (unexpected churn spike)?
- Is this data quality (missing data, system error)?

### 4. **Stable vs. Special Cause**

- **No rules triggered:** Your metric shows normal, random variation (common cause)
- **Rules triggered:** Something unusual is happening (special cause) that needs investigation

---

## Reading Your Weekly SPC Report

Each week, you'll receive a report showing:

1. **Executive Summary:** High-level overview of metric health
2. **Metric Details:** Current value, position relative to mean, and triggered rules
3. **Visual Charts:** XmR charts showing the data with control limits and zone lines
4. **Rule Explanations:** Which rules were triggered and what they mean

### Status Indicators

- **✅ Stable:** No rules triggered - metric is within normal variation
- **⚠️ Warning:** Minor rules triggered (Rule 3, Rule 5) - monitor closely
- **🚨 Alert:** Major rules triggered (Rule 1, Rule 2, Rule 4, MR violations) - investigate immediately

---

## Example: Interpreting a Chart

```
Churned Sound Zones - Feb 10, 2026
Current: 45 (above average)
Mean: 38.5 | Limits: [15.2, 61.8]

🚨 Rule 1: Beyond 3σ on Feb 8 — an extreme value outside normal operating range
⚠️ Rule 4: 8 same side from Feb 1-8 — a sustained shift in the process level
```

**What this tells you:**

1. There was a spike in churn on Feb 8 (Rule 1) that needs immediate investigation
2. Leading up to that spike, churn was consistently above average for 8 days (Rule 4)
3. The current churn rate (45) is elevated but within control limits
4. Action: Investigate what happened on Feb 8 and what changed starting Feb 1

---

## Best Practices

### ✅ Do:

- Investigate critical signals promptly
- Look for business context behind signals
- Update stakeholders when patterns are found
- Use SPC to guide data-driven decisions

### ❌ Don't:

- React to every small fluctuation (that's common cause variation)
- Ignore multiple consecutive signals
- Adjust control limits without understanding why the process changed
- Use SPC as a replacement for business judgment

---

## Additional Resources

- **Weekly Reports:** Check #spc-reports channel for automated weekly summaries
- **Questions:** Contact the Analytics team
- **Data Sources:** All metrics pulled from `StatisticalProcessControl.SPCKeyMetricsDaily`

---

_Last updated: February 11, 2026_
_Generated by Soundtrack Analytics SPC System_
