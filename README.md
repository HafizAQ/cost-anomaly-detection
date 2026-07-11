# Lab: Detect Unexpected AWS Costs with AWS Cost Anomaly Detection

**Estimated Time:** 60–90 minutes  
**Difficulty:** Beginner – Intermediate  
**Prerequisites:** AWS Account with Billing access, completed AWS Cost Management lesson

---

# Learning Objectives

By the end of this lab, you will be able to:

- Explain the purpose of AWS Cost Anomaly Detection
- Create an AWS Cost Anomaly Monitor
- Configure an email notification subscription
- Understand monitor scopes and monitor types
- Investigate detected anomalies
- Compare AWS Cost Anomaly Detection with AWS Budgets
- Recommend actions after receiving an anomaly alert

---

# Scenario

You have recently joined the Cloud Operations team at **CloudNova Solutions**.

Last month, the company received an AWS bill that was **five times higher** than expected because several expensive resources were accidentally left running over the weekend.

Management now wants an automated solution that can detect unusual spending patterns and notify the cloud team before costs become a serious problem.

Your task is to configure AWS Cost Anomaly Detection so that the finance and engineering teams receive alerts whenever AWS detects unexpected spending.

---

# Lab Overview

In this lab you will:

1. Explore AWS Cost Anomaly Detection
2. Create a Cost Monitor
3. Configure an Alert Subscription
4. Review anomaly detection settings
5. Investigate a sample anomaly
6. Compare Cost Anomaly Detection with AWS Budgets
7. Perform a FinOps investigation exercise

---

# Prerequisites

- AWS Free Tier Account
- Billing permissions
- Access to the Billing and Cost Management Console
- Valid email address

Recommended IAM Permissions:

- Billing
- Cost Explorer
- AWS Cost Anomaly Detection

---

# Architecture

```
AWS Services
        │
        ▼
Cost Explorer analyzes spending
        │
        ▼
Machine Learning builds baseline
        │
        ▼
Unexpected Cost Detected
        │
        ▼
Cost Anomaly Monitor
        │
        ▼
Email Notification
        │
        ▼
Cloud Operations Team investigates
```

---

# Part 1 – Explore AWS Cost Anomaly Detection

## Step 1 – Navigate to Cost Anomaly Detection

1. Sign in to the AWS Console.
2. Search for **Billing and Cost Management**.
3. From the left navigation menu select:

```
Cost Management
```

then

```
Cost Anomaly Detection
```

Explore the dashboard.

### Questions

- What problem does this service solve?
- How is it different from AWS Budgets?

---

### 📸 Screenshot Required

**Filename**

```
screenshots/01-cost-anomaly-dashboard.png
```

**Capture**

- AWS Cost Anomaly Detection dashboard
- Left navigation menu
- Dashboard overview

**Purpose**

Demonstrates that you successfully accessed the Cost Anomaly Detection service.

---

# Part 2 – Create a Cost Monitor

## Step 2 – Create a New Monitor

Click **Create Monitor**.

Configure:

| Setting | Value |
|----------|-------|
| Monitor Name | bootcamp-cost-monitor |
| Monitor Type | AWS Services |

Leave all remaining settings as default.

Click **Create Monitor**.

---

### 📸 Screenshot Required

**Filename**

```
screenshots/02-create-monitor.png
```

**Capture**

- Monitor name
- Monitor type
- Configuration before clicking **Create Monitor**

**Purpose**

Shows the monitor has been configured correctly.

---

After the monitor has been created:

### 📸 Screenshot Required

**Filename**

```
screenshots/03-monitor-created.png
```

**Capture**

- Newly created monitor
- Monitor status
- Monitor details page

**Purpose**

Verifies successful monitor creation.

---

## Understanding Monitor Types

Review the available monitor types.

| Monitor Type | Description |
|---------------|-------------|
| AWS Services | Monitors AWS service spending |
| Linked Account | Monitors one AWS account |
| Cost Category | Monitors a business unit |
| Tag | Monitors tagged resources |

Think about when each monitor type would be useful.

---

# Part 3 – Create an Email Subscription

## Step 3 – Configure Notifications

Open your monitor.

Click **Create Subscription**.

Configure:

| Setting | Value |
|----------|-------|
| Subscription Name | engineering-alerts |
| Frequency | Immediate |
| Threshold | $10 |
| Recipient | Your email address |

Click **Create Subscription**.

---

### 📸 Screenshot Required

**Filename**

```
screenshots/04-create-subscription.png
```

**Capture**

- Subscription configuration
- Frequency
- Threshold
- Recipient email (blur if desired)

**Purpose**

Shows the subscription is configured correctly.

---

After creating the subscription:

### 📸 Screenshot Required

**Filename**

```
screenshots/05-subscription-created.png
```

**Capture**

- Successful subscription
- Status
- Recipient

**Purpose**

Confirms the notification subscription exists.

---

# Part 4 – Explore the Monitor Dashboard

Open your monitor dashboard.

Observe:

- Active anomalies
- Historical anomalies
- Estimated financial impact
- Root cause analysis

If your AWS account is new, there may be no anomalies yet.

This is expected.

Answer:

- What information is shown for each anomaly?
- Can AWS determine the root cause automatically?

---

### 📸 Screenshot Required

**Filename**

```
screenshots/06-monitor-dashboard.png
```

**Capture**

- Dashboard
- Charts
- Anomalies (or empty state)

**Purpose**

Demonstrates you explored the monitor dashboard.

---

# Part 5 – Investigate a Sample Alert

Use the following simulated alert.

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

Answer:

1. Which AWS service caused the anomaly?
2. Is the increase expected?
3. Which AWS service would you investigate first?
4. List three actions you would perform immediately.
5. How could this have been prevented?

---

# Part 6 – Compare with AWS Budgets

Complete the table.

| Feature | AWS Budgets | Cost Anomaly Detection |
|----------|-------------|------------------------|
| Uses Machine Learning | | |
| Uses Fixed Thresholds | | |
| Detects Unexpected Spending | | |
| Sends Email Alerts | | |
| Learns Historical Spending | | |
| Predicts Unusual Behaviour | | |

---

# Part 7 – Real World Discussion

Determine whether each scenario would likely trigger an anomaly.

| Scenario | Alert? | Why? |
|----------|---------|------|
| One t3.micro instance | | |
| 40 EC2 instances | | |
| Four NAT Gateways | | |
| Multi-AZ RDS | | |
| Lambda increase by 10% | | |
| New Redshift Cluster | | |

---

# CLI Exploration

Although anomaly monitors are primarily configured through the AWS Console, Cost Explorer data can be queried using the AWS CLI.

```bash
aws ce get-cost-and-usage \
  --time-period Start=2026-07-01,End=2026-07-31 \
  --granularity MONTHLY \
  --metrics UnblendedCost
```

Questions:

- What information does this command return?
- Why can't this command create an anomaly monitor?

---

# Verification Checklist

- [ ] Opened AWS Cost Anomaly Detection
- [ ] Created a Cost Monitor
- [ ] Created an Email Subscription
- [ ] Verified notification settings
- [ ] Explored the monitor dashboard
- [ ] Completed the investigation exercise
- [ ] Compared Cost Anomaly Detection with AWS Budgets

---

# Bonus Challenges

## Challenge 1

Create another monitor for a linked AWS account.

---

## Challenge 2

Research the differences between:

- AWS Budgets
- Cost Anomaly Detection
- Cost Explorer

---

## Challenge 3

Design a FinOps monitoring strategy using:

- Cost Explorer
- AWS Budgets
- Cost Anomaly Detection
- AWS Trusted Advisor

---

# Common Issues

| Problem | Solution |
|----------|----------|
| Cannot access Billing | Missing IAM permissions |
| Cannot create monitor | Use the management account |
| No anomalies displayed | New accounts need historical billing data |
| Email not received | Confirm the email subscription |
| Empty dashboard | AWS has not built a spending baseline yet |

---

# Cleanup

Delete:

1. Email Subscription
2. Cost Monitor

Verify that no Cost Anomaly Detection resources remain.

---

# Key Takeaways

- AWS Cost Anomaly Detection uses machine learning to establish a normal spending baseline.
- It automatically detects unusual spending patterns.
- Email alerts allow teams to react quickly.
- It complements AWS Budgets instead of replacing them.
- Together, these services form the foundation of a FinOps monitoring strategy.

---

# Next Steps

In the next lab you will:

- Create AWS Budgets
- Configure budget notifications
- Compare budgets with anomaly detection
- Build a proactive AWS cost monitoring solution

---

# Congratulations!

You have successfully configured AWS Cost Anomaly Detection and implemented your first automated FinOps cost monitoring solution.
