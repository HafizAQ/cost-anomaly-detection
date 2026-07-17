# Lab Solution: Detect Unexpected AWS Costs with AWS Cost Anomaly Detection

**Student Name:** Hafiz Abdul Quddus

**Date:** 17-07-2026

**Lab Completion Time:** 100 minutes

---

# Part 1 – Explore AWS Cost Anomaly Detection

## Questions

### 1. What problem does AWS Cost Anomaly Detection solve?

**Your Answer**

```
AWS Cost Anomaly Detection helps identify unexpected or unusual increases in AWS spending by continuously monitoring usage costs 
with machine learning. It automatically detects cost anomalies and sends alerts, allowing users to investigate and resolve issues 
before they result in significant unexpected charges.
```

---

### 2. How is it different from AWS Budgets?

**Your Answer**

```
AWS Cost Anomaly Detection automatically detects unexpected spending patterns using machine learning and alerts users when unusual 
costs occur. In contrast, AWS Budgets allows users to set predefined cost or usage limits and sends notifications only when those 
budget thresholds are reached or exceeded.
```

---

## Screenshot 1 – Cost Anomaly Detection Dashboard

Save your screenshot as:

```
screenshots/01-cost-anomaly-dashboard.png
```

![Cost Anomaly Dashboard](screenshots/01-cost-anomaly-dashboard.png)

---

# Part 2 – Create a Cost Monitor

## Monitor Configuration

| Setting      | Your Value                    |
| ------------ | ----------------------------- |
| Monitor Name | bootcamp-cost-monitor         |
| Monitor Type | AWS Services (Linked account) |

---

## Screenshot 2 – Monitor Configuration

Save your screenshot as:

```
screenshots/02-create-monitor.png
```

![Create Monitor](screenshots/02-create-monitor.png)

---

## Monitor Details

| Item           | Value                                 |
| -------------- | ------------------------------------- |
| Monitor Name   | bootcamp-cost-monitor                 |
| Monitor Status | Monitor has been created successfully |
| Monitor Scope  | Anomalies detection w.r.t Cost        |

---

## Screenshot 3 – Monitor Created

Save your screenshot as:

```
screenshots/03-monitor-created.png
```

![Monitor Created](screenshots/03-monitor-created.png)

---

# Part 3 – Create an Email Subscription

## Subscription Details

| Setting           | Your Value              |
| ----------------- | ----------------------- |
| Subscription Name | engineering-alerts      |
| Frequency         | Daily                   |
| Threshold         | 10$                     |
| Recipient Email   | hafiz-XXXXX@outlook.com |

---

## Screenshot 4 – Subscription Configuration

Save your screenshot as:

```
screenshots/04-create-subscription.png
```

![Subscription Configuration](screenshots/04-create-subscription.png)

---

## Screenshot 5 – Subscription Created

Save your screenshot as:

```
screenshots/05-subscription-created.png
```

![Subscription Created](screenshots/05-subscription-created.png)

---

# Part 4 – Explore the Monitor Dashboard

## Dashboard Observations

### What information is displayed for each anomaly?

```
Each anomaly shows the affected service, estimated cost impact, time period, and the possible cause.
```

---

### Can AWS automatically determine the root cause?

```
No. AWS suggests possible causes, but users must investigate to confirm the exact root cause. Anomaly detection monitor could help to faster this process.
```

---

## Screenshot 6 – Monitor Dashboard

Save your screenshot as:

```
screenshots/06-monitor-dashboard.png
```

![Monitor Dashboard](screenshots/06-monitor-dashboard.png)

---

# Part 5 – Investigate a Sample Alert

## Scenario

```
Expected Spend

$18.25

Actual Spend

$241.87

Difference

+$223.62

Primary Service

Amazon EC2

Region

us-east-1

Estimated Cause

15 m6i.large instances launched
```

---

## Question 1

Which AWS service caused the anomaly?

```
Amazon EC2
```

---

## Question 2

Is this increase expected or unexpected? Explain your reasoning.

```
No, it appears unexpected.
```

---

## Question 3

Which AWS Console page would you investigate first?

```
Amazon EC2
```

---

## Question 4

List at least three actions you would perform immediately.

```
Check the running EC2 instances.
```

```
Stop or terminate unnecessary instances.
```

```
Review who launched the instances and when.
```

---

## Question 5

How could this situation have been prevented?

```
By enabling Cost Anomaly Detection, setting AWS Budgets, and monitoring EC2 usage regularly.
```

---

# Part 6 – Compare with AWS Budgets

Complete the following table.

| Feature                     | AWS Budgets | Cost Anomaly Detection |
| --------------------------- | ----------- | ---------------------- |
| Uses Machine Learning       | No          | Yes                    |
| Uses Fixed Thresholds       | Yes         | No                     |
| Detects Unexpected Spending | No          | Yes                    |
| Sends Email Alerts          | Yes         | Yes                    |
| Learns Historical Spending  | No          | Yes                    |
| Predicts Unusual Behaviour  | No          | Yes                    |

---

# Part 7 – Real World Discussion

Complete the table below.

| Scenario                        | Would it trigger an alert? | Why?                                                   |
| ------------------------------- | -------------------------- | ------------------------------------------------------ |
| Launch one t3.micro instance    | No                         | Cost increase is very small (Free Tier basic package)) |
| Launch 40 EC2 instances         | Yes                        | Causes a large, unusual cost increase.                 |
| Create four NAT Gateways        | Yes                        | NAT Gateways are expensive and increase costs.         |
| Multi-AZ RDS Database           | Yes                        | Running multiple database instances increases cost.    |
| Lambda traffic increases by 10% | No                         | A small increase is usually considered normal.         |
| Create a Redshift Cluster       | Yes                        | Redshift clusters have high running costs.             |


---

# CLI Exploration

## AWS CLI Command Used

```bash
aws ce get-cost-and-usage \
  --time-period Start=2026-07-01,End=2026-07-31 \
  --granularity MONTHLY \
  --metrics UnblendedCost


  #Output 
  {
    "ResultsByTime": [
        {
            "TimePeriod": {
                "Start": "2026-07-01",
                "End": "2026-07-31"
            },
:...skipping...
{
    "ResultsByTime": [
        {
            "TimePeriod": {
                "Start": "2026-07-01",
                "End": "2026-07-31"
            },
            "Total": {
:...skipping...
{
    "ResultsByTime": [
        {
            "TimePeriod": {
                "Start": "2026-07-01",
                "End": "2026-07-31"
            },
```

---

### What information did this command return?

```
The command returned the monthly AWS cost data for the period 2026-07-01 to 2026-07-31, 
including the total UnblendedCost for that month.
```

---

### Why can't this command create Cost Anomaly Monitors?

```
Because the `get-cost-and-usage` command is read-only. It only retrieves cost information 
and cannot create or manage Cost Anomaly Monitors.
```

---

# Reflection Questions

## 1. Why is Cost Anomaly Detection considered a proactive FinOps tool?

```
It detects unusual spending early, helping prevent higher costs.
```

---

## 2. Why should organizations use both AWS Budgets and Cost Anomaly Detection?

```
Budgets track spending limits, while Cost Anomaly Detection finds unexpected costs.
```

---

## 3. What types of AWS resources are most likely to trigger anomalies?

```
EC2 instances, RDS databases, NAT Gateways, and Redshift clusters.
```

---

## 4. How would you investigate an unexpected AWS bill?

```
Check Cost Explorer, review recent resource changes, and stop unnecessary resources.
```

---

## 5. What would you do if you received a Cost Anomaly alert at 2:00 AM?

```
Review the alert immediately, identify the cause, and stop unnecessary resources if needed.
```

---

# Verification Checklist

- [X] Successfully accessed AWS Cost Anomaly Detection
- [X] Created a Cost Monitor
- [X] Created an Email Subscription
- [X] Verified notification settings
- [X] Explored the dashboard
- [X] Completed the investigation exercise
- [X] Compared AWS Budgets with Cost Anomaly Detection
- [X] Completed all reflection questions

---

# Troubleshooting Log

Did you encounter any issues?

☐ Yes

☐ No

If yes, document them below.

| Issue | Resolution |
| ----- | ---------- |
|       |            |
|       |            |
|       |            |

---

# Bonus Challenges Completed : NA

- [ ] Challenge 1 – Created another Cost Monitor
- [ ] Challenge 2 – Compared AWS Budgets, Cost Explorer, and Cost Anomaly Detection
- [ ] Challenge 3 – Designed a FinOps monitoring strategy

---

## Bonus Notes

```
_______________________________________________________________

_______________________________________________________________

_______________________________________________________________
```

---

# Cleanup Confirmation

- [ ] Deleted Email Subscription
- [ ] Deleted Cost Monitor
- [ ] Verified no monitors remain

---

# Self Assessment

Rate your confidence for each topic.

| Topic                           | Rating (1–5) |
| ------------------------------- | ------------- |
| Cost Anomaly Detection Concepts | ____          |
| Creating Cost Monitors          | ____          |
| Creating Alert Subscriptions    | ____          |
| Investigating Cost Anomalies    | ____          |
| Comparing with AWS Budgets      | ____          |
| FinOps Best Practices           | ____          |

---

# Instructor Verification

**Instructor Name:** __________________________________

**Date Reviewed:** ____________________________________

**Comments**

```
_______________________________________________________________

_______________________________________________________________

_______________________________________________________________
```

**Status**

☐ Complete

☐ Needs Revision

☐ Excellent

---

# Time Tracking

| Activity               | Minutes |
| ---------------------- | ------- |
| Reading Lab            | ______  |
| Creating Monitor       | ______  |
| Creating Subscription  | ______  |
| Investigation Exercise | ______  |
| Reflection Questions   | ______  |

---

# Lab Status

☐ Complete

☐ In Progress

☐ Needs Revision

**Submission Date:**  17-07-2026
