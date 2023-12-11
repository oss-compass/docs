---
title: Contributor Milestone Persona
slug: /metrics-models/people/productivity/contributor-milestone-persona
tags:
  - Metrics Models
  - people
  - Productivity
  - Contributor Milestone Persona
---

# Contributor Milestone Persona

Contributors may resonate with open source projects based on upstream or downstream ecological interests, personal development, etc., and engage in community contributions. They may stay in the community for a long time, gradually fade away, or even be reawakened. Based on these scenarios, we define various states of contributors in the community, forming the Milestone Persona Model. This model is inspired by a state machine, where contributors can transition between states, but they can only be in one state at a time. This ensures decoupling of behavior and is more conducive to observing contributors' actions in the community.

![image](https://github.com/oss-compass/docs/assets/53640896/6fd6531d-5dc7-4f93-9c92-d35e8c2db0c2)

Based on contributors' contribution amount, contribution frequency, contribution type, and their states in the community, and considering the time period of contributors' milestones, we divide contributors' milestones into the above 5 states (Figure 5): no state, visitors, regulars, core, and silent. Taking the annual period as an example, here are the definitions of the five states:

- Core: Refers to contributors who complete 50% of all domain contributions in the current year (excluding observer-type contributions such as stars, forks, and watches). These contributions are completed by at least one group of people, referred to as core contributors. All domain contributions are not weighted, only the count is considered.
- Regulars: After excluding the 50% contributions made by core contributors, the next 30% contributions (excluding observer-type contributions such as stars, forks, and watches), completed by at least one group of people. These contributors have been involved in contributions for at least 9 months in the current year and are referred to as regular contributors.
- Visitors: After excluding core and regular contributions, contributors involved in the remaining community contributions (including observer-type contributions, i.e., stars, forks, and watches) are referred to as visitors.
- Silent: Contributors who were active as core, regular, or visitors in the previous year but have made no contributions in the current year.
- No State: People who have never made contributions in the community.

# Metrics in the Metrics Model

## Core Contributor Count

- Definition: How many active core contributors in the last 90 days.
- Weight: 20%
- Threshold: 20

## Core Contribution Count

- Definition: The number of contributions per capita for contributors in the active core in the last 90 days.
- Weight: 30%
- Threshold: 200

## Regular Contributor Count

- Definition: How many active regular contributors in the last 90 days.
- Weight: 12%
- Threshold: 100

## Regular Contribution Count

- Definition: The number of contributions per capita for contributors in the active regular in the last 90 days.
- Weight: 18%
- Threshold: 25

## Visitor Contributor Count

- Definition: How many active visitor contributors in the last 90 days.
- Weight: 8%
- Threshold: 2000

## Visitor Contribution Count

- Definition: The number of contributions per capita for contributors in the active visitor in the last 90 days.
- Weight: 12%
- Threshold: 5

# Metric Model Algorithm

## Weight

We use [AHP](https://en.wikipedia.org/wiki/Analytic_hierarchy_process) to calculate weight of each metric.

### AHP Input Data

| Metric Name                | Core Contributor Count | Core Contribution Count | Regular Contributor Count | Regular Contribution Count | Visitor Contributor Count | Visitor Contribution Count |
| -------------------------- | ---------------------- | ----------------------- | ------------------------- | -------------------------- | ------------------------- | -------------------------- |
| Core Contributor Count     | 1.000                  | 0.667                   | 1.667                     | 1.111                      | 2.500                     | 1.667                      |
| Core Contribution Count    | 1.500                  | 1.000                   | 2.500                     | 1.667                      | 3.750                     | 2.500                      |
| Regular Contributor Count  | 0.600                  | 0.400                   | 1.000                     | 0.667                      | 1.500                     | 1.000                      |
| Regular Contribution Count | 0.900                  | 0.600                   | 1.500                     | 1.000                      | 2.250                     | 1.500                      |
| Visitor Contributor Count  | 0.400                  | 0.267                   | 0.667                     | 0.444                      | 1.000                     | 0.667                      |
| Visitor Contribution Count | 0.600                  | 0.400                   | 1.000                     | 0.667                      | 1.500                     | 1.000                      |

### AHP Analysis Result

| Metrics Name               | Eigenvector | Weight  |
| -------------------------- | ----------- | ------- |
| Core Contributor Count     | 1.200       | 20.000% |
| Core Contribution Count    | 1.800       | 30.000% |
| Regular Contributor Count  | 0.720       | 12.000% |
| Regular Contribution Count | 1.080       | 18.000% |
| Visitor Contributor Count  | 0.480       | 8.000%  |
| Visitor Contribution Count | 0.720       | 12.000% |

### Consistency Test Results

| Largest Eigenvalue | CI Value | RI Value | CR Value | Consistency Test |
| ------------------ | -------- | -------- | -------- | ---------------- |
| 6.000              | 0.000    | 1.260    | 0.000    | PASS             |

## Threshold

The threshold we chose is based on the big-data observations from different types of open source projects.

# References

- [Reflections on the Evaluation and Measurement of Open Source Ecosystem (1) — Evolution and Trends](https://oss-compass.org/blog/2023/12/07/open-source-eco1/open-source-eco1)
- [ Reflections on the Evaluation and Measurement of Open Source Ecosystem (2) - The Multidimensional Space of Evaluation Systems](https://oss-compass.org/blog/2023/12/08/open-source-eco2/open-source-eco2)
- [Reflections on the Evaluation and Measurement of Open Source Ecosystem (3) - Dynamics and Statics of Contributors](https://oss-compass.org/blog/2023/12/09/open-source-eco3/open-source-eco3)

# Contributors

## Frontend

- Shengxiang Zhang
- Feng Zhong
- Xingyou Lai

## Backend

- Yehui Wang
- Shengxiang Zhang
- Shengbao Li
- Huatian Qin

## Metric Model

- Yehui Wang
- Liang Wang
- Shengbao Li
