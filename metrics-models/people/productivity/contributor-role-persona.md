---
title: Contributor Role Persona
slug: /metrics-models/people/productivity/contributor-role-persona
tags:
  - Metrics Models
  - people
  - Productivity
  - Contributor Role Persona
description: 
---

# Contributor Role Persona

The initiation of open source projects is usually carried out by a team or an individual, initiating and establishing in their personal or organizational capacity. In the evolutionary process, new individuals or organizations are continuously brought in to make contributions. Whether they are initiators or later joiners, through establishing mutually beneficial cooperation with the community and making prominent and sustained contributions, they gain roles of community managers. This role can usually be demonstrated by performing certain management actions on code hosting platforms. We also use this type of event behaviors to identify whether contributors have a managerial role. Contributors who are not perceived to have managing behaviors are called Participants.

We use the term Managers to describe contributors in the community who have management privileges. Typically, they are also technical leaders of the projects. However, technical leadership does not necessarily equate to management actions, so we use the more specific term "manager" for clarity.

Determining whether a contributor is a manager is based on whether they have made contributions in issue management or code management categories. Of course, a contributor may not be a manager when initially participating in community contributions, so we introduce timestamps to mark the change in this role. In the two contribution categories mentioned above, if contributors declare their organizational identities, such as by forcefully submitting code through a public organizational email, we refer to them as organizational managers; otherwise, they are considered individual managers.

![image](https://github.com/oss-compass/docs/assets/53640896/4e37feaf-0831-4add-864d-3b3911ea991b)

- Managers:
  - Organizational Managers
  - Individual Managers
- Participants:
  - Organizational Participants
  - Individual Participants




# Metrics in the Metrics Model

## Organizational Contributor Count

* Definition: How many active organizational contributors in the last 90 days.
* Weight: 20%
* Threshold: 1500

## Organizational Contribution Count

* Definition: The number of contributions per capita for contributors in the active organizational in the last 90 days.
* Weight: 30%
* Threshold: 10

## Individual Contributor Count

* Definition: How many active individual contributors in the last 90 days.
* Weight: 20%
* Threshold: 3500

## Individual Contribution Count

* Definition: The number of contributions per capita for contributors in the active individual in the last 90 days.
* Weight: 30%
* Threshold: 5



# Metric Model Algorithm

## Weight

We use [AHP](https://en.wikipedia.org/wiki/Analytic_hierarchy_process) to calculate weight of each metric.

### AHP Input Data

Metric Name  | Organizational Contributor Count | Organizational Contribution Count | Individual Contributor Count | Individual Contribution Count |
| --- | --- | --- | --- | --- |
| Organizational Contributor Count | 1.000 | 0.667 | 1.000 | 0.667 |
| Organizational Contribution Count | 1.500 | 1.000 | 1.500 | 1.000 |
| Individual Contributor Count | 1.000 | 0.667 | 1.000 | 0.667 |
| Individual Contribution Count | 1.500 | 1.000 | 1.500 | 1.000 |


### AHP Analysis Result

Metrics Name | Eigenvector | Weight
--- | --- | ---
| Organizational Contributor Count | 0.800 | 20.000% |
| Organizational Contribution Count | 1.200 | 30.000% |
| Individual Contributor Count | 0.800 | 20.000% |
| Individual Contribution Count | 1.200 | 30.000% |

### Consistency Test Results

Largest Eigenvalue | CI Value | RI Value| CR Value | Consistency Test
--- | --- | --- | --- | ---
| 4.000 | 0.000 | 0.890 | 0.000 | PASS    |

## Threshold

The threshold we chose is based on the big-data observations from different types of open source projects.

# References

* [Reflections on the Evaluation and Measurement of Open Source Ecosystem (1) — Evolution and Trends](https://oss-compass.org/blog/2023/12/09/open-source-eco1/open-source-eco1)
* [ Reflections on the Evaluation and Measurement of Open Source Ecosystem (2) - The Multidimensional Space of Evaluation Systems](https://oss-compass.org/blog/2023/12/09/open-source-eco2/open-source-eco2)
* [Reflections on the Evaluation and Measurement of Open Source Ecosystem (3) - Dynamics and Statics of Contributors](https://oss-compass.org/blog/2023/12/09/open-source-eco3/open-source-eco3)

# Contributors
## Frontend

* Shengxiang Zhang
* Feng Zhong
* Xingyou Lai

## Backend

* Yehui Wang
* Shengxiang Zhang
* Shengbao Li
* Huatian Qin

## Metric Model

* Yehui Wang
* Liang Wang
* Shengbao Li