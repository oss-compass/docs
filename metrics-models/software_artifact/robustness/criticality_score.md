---
title: Criticality Score
slug: /metrics-models/software_artifact/robustness/criticality_score
tags:
  - Metrics Model
  - Software Artifact
  - Robustness
  - Criticality Score
description: A criticality scoring model for assessing the influence and importance of open source projects.
---

# Criticality Score

This model is based on the implementation of the [OpenSSF Criticality Score project](https://github.com/ossf/criticality_score) to generate a criticality score for each open source project, create a list of critical projects, and use this data to proactively improve the security of these critical projects.

# Metrics in the Metrics Model

## Creation Time

- Definition: The time since the project was created (in months).
- Weight: 9.523%
- Threshold: 120

Older projects have a higher chance of being widely used or depended upon by other projects.

## Update Time

- Definition: The time since the project was last updated (in months).
- Weight: -9.523%
- Threshold: 120

Unmaintained projects with no recent commits are less likely to be depended upon.

## Contributor Count

- Definition: The number of contributors to the project (with commit history).
- Weight: 19.047%
- Threshold: 5000

Participation from different contributors indicates the importance of the project.

## Organization Count

- Definition: The number of different organizations to which the contributors belong.
- Weight: 9.523%
- Threshold: 10

Indicates cross-organizational dependencies.

## Commit Frequency

- Definition: The average number of commits per week over the past year.
- Weight: 9.523%
- Threshold: 1000

A higher rate of code changes slightly indicates the importance of the project. It is also more susceptible to vulnerabilities.

## Recent Release Count

- Definition: The number of releases in the past year.
- Weight: 4.761%
- Threshold: 26

Frequent releases indicate user dependency. The weight is lower because this is not always used.

## Closed Issue Count

- Definition: The number of closed issues in the past 90 days.
- Weight: 4.761%
- Threshold: 5000

Indicates high contributor involvement and a focus on closing user issues. The weight is lower because it depends on project contributors.

## Updated Issue Count

- Definition: The number of updated issues in the past 90 days.
- Weight: 4.761%
- Threshold: 5000

Indicates high contributor involvement. The weight is lower because it depends on project contributors.

## Comment Frequency

- Definition: The average number of comments per issue in the past 90 days.
- Weight: 9.523%
- Threshold: 15

Indicates user activity and dependencies.

## Dependent Count

- Definition: The number of times the project is mentioned by other projects in commit messages.
- Weight: 19.047%
- Threshold: 50

Indicates repository usage, often in version updates. This parameter applies to all languages.

# Metrics Model Algorithm

## Model Weights and Thresholds

We use the following parameters to calculate the criticality score of an open source project:

| Metric Name (S<sub>i</sub>) | Weight (&alpha;<sub>i</sub>) | Threshold (T<sub>i</sub>) | Definition |
|---|---|---|---|
| Creation Since | 9.523% | 120 | The time since the project was created (in months) |
| Update Since | -9.523% | 120 | The time since the project was last updated (in months) |
| Contributor Count | 19.047% | 5000 | The number of contributors to the project (with commit history) |
| Org Count | 9.523% | 10 | The number of different organizations to which the contributors belong |
| Commit Frequency | 9.523% | 1000 | The average number of commits per week over the past year |
| Recent Releases Count | 4.761% | 26 | The number of releases in the past year |
| Closed Issues Count | 4.761% | 5000 | The number of closed issues in the past 90 days |
| Updated Issues Count | 4.761% | 5000 | The number of updated issues in the past 90 days |
| Comment Frequency | 9.523% | 15 | The average number of comments per issue in the past 90 days |
| Dependents Count | 19.047% | 50 | The number of times the project is mentioned by other projects in commit messages |

## Score Calculation

The criticality score of an open source project defines its influence and importance. It is a number between 0 (least critical) and 1 (most critical). The score is based on an [algorithm](https://github.com/ossf/criticality_score/blob/main/Quantifying_criticality_algorithm.pdf) proposed by [Rob Pike](https://github.com/robpike):

<img src="https://raw.githubusercontent.com/ossf/criticality_score/main/images/formula.png" width="359" height="96">

Where:
- &alpha;i is the weight of each metric
- Si is the actual value of each metric
- Ti is the maximum threshold for each metric


# References

- [OpenSSF Criticality Score](https://github.com/ossf/criticality_score)
- [Quantifying Criticality Algorithm](https://github.com/ossf/criticality_score/blob/main/Quantifying_criticality_algorithm.pdf)
- [Securing Critical Projects WG](https://github.com/ossf/wg-securing-critical-projects)


# Contributors

## Backend

- Yehui Wang
- Shengbao Li

## Metrics Model

- Yehui Wang
- Guoqiang Qi
- Shengbao Li