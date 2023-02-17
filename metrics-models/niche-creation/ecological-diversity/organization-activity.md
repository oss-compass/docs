---
title: Organizations Activity
slug: /metrics-models/niche-creation/organization-activity
tags:
  - Metrics Models
  - Niche Creation
  - Organizations Activity
description: Describe how active organizations are in a community.
---

# Organizations Activity

 Organizational activity is used to assess the activity of organizations in the community (Business Companies, colleges, etc.) . For an open source project, especially for a platform-based software project, the more organizations participate in community contributions, indicating that the ecological construction of the community is towards prosperity. Because software projects provide the business value or academic value-binding that organizations need, organizations are willing to participate in community contributions using organizations identities.

## Metrics in the Metrics Model

### Org Count

* Definition: Number of organizations to which active code contributors belong in the past 90 days
* Weight: 32.258%
* Threshold: 30

What we count here are the organizations that contribute code. The reason for only counting code contributions is that code contributions have the highest technical threshold compared to other types of community contributions, and are the most direct manifestation of an organization's participation in community contributions. At the same time through the analysis of the organization's categories, we can also be more in-depth insight, such as understanding of the project's north-south ecological construction, etc.

### Org Contributor Count

* Definition: Number of active code contributors with organization affiliation in the past 90 days
* Weight: 25.806%
* Threshold: 300

Here we count the number of code contributors with organized attributes. We are here to examine the organization's continued investment in community human resources.

### Org Commit Frequency

* Definition: Determine the average number of commits with organization affiliation per week in the past 90 days.
* Weight: 25.81%
* Threshold: 800

This indicator is similar to the number of contributors and measures the organization's input to the community in terms of the number of code contributions.

### Org Contribution Last

* Definition: Total contribution time of all organizations to the community in the past 90 days (weeks).
* Weight: 16.13%
* Threshold: 200

We look at the development of ecology in terms of the time dimension, through how the organization participates and invests as time goes by.

## Metric Model Algorithm

### Weight

We use [AHP](https://en.wikipedia.org/wiki/Analytic_hierarchy_process) to calculate weight of each metric.

#### AHP Input Data

Metric Name | Org Count | Contributor Count | Commit Frequency | Contribution Last 
--- | --- | --- | --- | ---
Org Count | 1.000 | 1.250 | 1.250 | 2.000
Contributor Count |  0.800 | 1.000 | 1.000 | 1.600
Commit Frequency |   0.800 | 1.000 | 1.000 | 1.600
Contribution Last |  0.500 | 0.625 | 0.625 | 1.000

#### AHP Analysis Result

Metrics Name | Eigenvector | Weight
--- | --- | ---
Org Count |   1.290 | 32.258%
Contributor Count |  1.032 | 25.806%
Commit Frequency |   1.032 | 25.806%
Contribution Last |  0.645 | 16.129%

#### Consistency Test Results

Largest Eigenvalue | CI Value | RI Value| CR Value | Consistency Test
--- | --- | --- | --- | ---
4.000 | 0.000 | 0.890 | 0.000  | PASS

### Threshold

The threshold we chose is based on the big-data observations from different types of open source projects.

<!-- ## References

* [CHAOSS Metric Model: Organizations Activity](https://github.com/chaoss/wg-metrics-models/tree/main/metrics-model-libs/organization-activity) 
-->
## Contributors

### Frontend

* Shengxiang Zhang
* Feng Zhong
* Chaoqun Huang
* Huatian Qin
* Xingyou Lai

### Backend

* Yehui Wang
* Shengbao Li
* Huatian Qin

### Metric Model

* Yehui Wang
* Shengbao Li