# AI/ML for Cybersecurity Lab 01: Brute-Force Classification

## Scenario0

You are a SOC analyst reviewing authentication events.  
The goal of this lab is to learn how basic machine learning concepts apply to cybersecurity without using heavy Python.

This lab focuses on:

- Features
- Labels
- Classification
- Normal vs Attack behavior
- False positives and false negatives
- Analyst investigation thinking

---

## Dataset

File:

```text
auth_ml_dataset.csv
```

Each row represents summarized authentication activity for a user.

---

## Dataset Fields

| Field | Meaning |
|---|---|
| timestamp | Time of the authentication activity |
| user | Username involved in the activity |
| src_ip | Source IP address |
| failed_logins | Number of failed login attempts |
| new_ip | Whether the IP is new for that user |
| successful_login_after_failures | Whether a successful login occurred after many failures |
| label | Known classification: Normal or Attack |

---

## ML Concept

This is a **supervised classification** lab because the dataset already contains labels:

```text
Normal
Attack
```

A model can learn from labeled examples.

Example:

```text
Small failed_logins + known IP = usually Normal
Large failed_logins + new IP = likely Attack
```

---

## SOC Question 1

Which users have the highest failed login counts?

### Analyst Goal

Identify possible brute-force or password attack activity.

---

## SOC Question 2

Which events are labeled as Attack?

### Analyst Goal

Understand what patterns separate Attack events from Normal events.

---

## SOC Question 3

Which features are most useful for classification?

Possible features:

```text
failed_logins
new_ip
successful_login_after_failures
```

---

## SOC Question 4

Which event could be a false positive?

Hint:

Look for an event that has many failed logins but may have a normal explanation.

---

## SOC Question 5

Which event is most dangerous?

Hint:

Look for:

```text
High failed_logins
new_ip = Yes
successful_login_after_failures = Yes
```

---

## Expected Analyst Findings

### Finding 1

The users with the highest failed login counts are:

```text
admin
root
guest
```

These should be investigated first.

---

### Finding 2

The strongest attack indicators are:

```text
High failed_logins
New source IP
Successful login after many failures
```

---

### Finding 3

The event involving:

```text
admin
failed_logins = 70
new_ip = Yes
successful_login_after_failures = Yes
```

is highly suspicious because it may indicate that the attacker eventually guessed the password.

---

### Finding 4

The event involving:

```text
service_backup
failed_logins = 35
new_ip = No
label = Normal
```

could represent a misconfigured service account instead of a real attack.

This teaches an important lesson:

> Not every unusual event is malicious.

---

## ML Vocabulary Used in This Lab

### Feature

A data field used to make a decision.

Examples:

```text
failed_logins
new_ip
successful_login_after_failures
```

### Label

The known answer.

Examples:

```text
Normal
Attack
```

### Classification

Predicting a category.

Example:

```text
Normal or Attack
```

### False Positive

A normal event incorrectly classified as an attack.

### False Negative

A real attack incorrectly classified as normal.

---

## GitHub Summary

This lab demonstrates how AI/ML classification concepts apply to cybersecurity authentication logs.  
The analyst uses features such as failed login count, new source IP, and successful login after failures to classify activity as Normal or Attack.

---

## Tools Required

No tools are required for the first version of this lab.

Optional tools for future versions:

- Excel or Google Sheets
- Splunk Enterprise
- Python with pandas
- scikit-learn

---

## Next Lab

AI/ML for Cybersecurity Lab 02:

```text
Anomaly Detection for Data Exfiltration
```

This next lab will focus on detecting unusually high outbound network traffic.
