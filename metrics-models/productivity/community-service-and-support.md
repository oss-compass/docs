---
title: Community Service and Support
slug: /metrics-models/productivity/community-service-and-support
tags:
  - Metrics Models
  - Productivity
  - Community Service and Support
description: Community Service and Support measures the quality of services and support provided by the community as directly perceived by a developer during the contribution process.
---

# Community Service and Support

Community Service and Support measures the quality of services and support provided by the community as directly perceived by a developer during the contribution process. The emphasis on direct perception comes from the fact that many of the underlying services provided by the community, such as the Devops infrastructure involved in the development, are also key elements in building community services, but are difficult for the community participants to perceive. At the same time, they are also lack of a universal means of assessment. We use the metric dimension that participants perceive in community-based development to indirectly evaluate the community's entire "Marathon-like logistic system in open source contribution". It should be noted that this does not mean that only the metrics mentioned in the model are sufficient, in order to ensure the independence of indicators, the model has done a strong correlation index dimension reduction; So if you want to maintain the long-term positive development of the model, the community's efforts go far beyond what the current metrics contain.

## Metrics in the Metrics Model

### Updated Issues Count

* Definition: Determine the number of issues updated in the last 90 days.
* Weight: 19.721%
* Threshold: 2000

There are two reasons why we chose to use the number of Issue updates instead of counting the number of issues that were closed or resolved. First, there are many different types of issues, such as bugs, new function requirements, user inquiries, and CVEs. Only certain types of problems, such as CVES, must be resolved quickly. For other types of issues, quick Issue resolution is not pursued usually, and we need to communicate with the issue creator multiple times to better understand the details that takes time. If the functional requirements, from acceptance to resolution, are in accordance with the release plan, such scenarios may also take several months. Second, from the number of Issue updates, we can monitor the activity of the Issue processing. The issue update can also include reopening the issue, indicating concern about changes in the understanding of the issue.

### Close PR Count

* Definition: The number of PR accepted and declined in the last 90 days.
* Weight: 19.721%
* Threshold: 4500

The more code you contribute, the more PR requests you need to close (accept or reject) . This indicates that the community is actively dealing with the PR. We use this metric together with [Close PR Count](#close-pr-count) as an outcome measure of the model, to provide an overall view of community service and support.

### Issue First Response

* Definition: Average/Median first comments response (in days) for new issues created in the last 90 days. This excludes bot responses,, the creator's own comment, or an action assigned by the issue. If the issue has been unanswered, the first response time is not counted.
* Weight: 14.372%
* Threshold: 15 days

We use this indicator to sense "Community temperature". And for contributors who join the community, if their questions are answered in a timely manner by the community, there's a good chance that they would be retained and continue to contribute to the community (according to [Mozilla Research](https://docs.google.com/presentation/d/1hsJLv1ieSqtXBzd5YZusY-mB8e1VJzaeOmh8Q4VeMio/edit#slide=id.g43d857af8_0177)) . At the same time, we found that more and more robots have been used to assist with Issue processing in recent years, so we eliminated robot interference and focused on human replies.

### Bug Issue Open Time

* Definition: Average/Median time (days) that bug issues have been opened for issues created in the last 90 days.
* Weight: 12.88%
* Threshold: 60 days
* Note: Issue that labeled by Bugs.

The Bug type Issue represents how efficiently the community handles issues that need to be resolved quickly. We chose to use Bug Issue to represent this type of Issues, which of course has its limitations, because not all bugs are high-priority ones, but rather than not distinguishing the Issue types, this index has some representativeness.

### PR Open Time

* Definition: Average/Median processing time (days) for new change requests created in the last 90 days, including closed/accepted change requests and unresolved change requests.
* Weight: 12.88%
* Threshold: 30 days

We are seeking for the change request fast close, including code merged or rejected. Otherwise the longer it takes for a change request to be resolved, the greater the risk that merge-conflict will occur, while other change requests that depend on it will also be stalled. 

### Issue Comment Frequency

* Definition: Determine the average number of comments per issue created in the last 90 days.
* Weight: 10.217%
* Threshold: 5

We would like to see the community encourage open and transparent discussion around specific bugs or requirements through Issue. The corresponding conclusions of the Issue can also be accumulated as a knowledge base and made available to more people.

### Code Review Count

* Definition: Determine the average number of review comments per pull request created in the last 90 days.
* Weight: 10.217%
* Threshold: 8

We hope that code could be reviewed publicly by PR that shows how much the community values code quality and security management, and helps new people grow quickly.

## Metric Model Algorithm

### Weight

We use [AHP](https://en.wikipedia.org/wiki/Analytic_hierarchy_process) to calculate weight of each metric.

#### AHP Input Data

Metric Name | Updated Issues Count | Close PR Count | Issue First Response | Bug Issue Open Time | PR Open Time | Comment Frequency | Code Review Count
--- | --- | --- | --- | --- | --- | --- | ---
Updated Issues Count|    1.000 | 1.000 | 1.333 | 1.500 | 1.500 | 2.000 | 2.000
Close PR Count        |   1.000 |  1.000 | 1.333 | 1.500 | 1.500 | 2.000 | 2.000
Issue First Response |   0.750 | 0.750 | 1.000 | 1.143 | 1.143 | 1.333 | 1.333
Bug Issue Open Time |    0.667 | 0.667 | 0.875 | 1.000 | 1.000 | 1.250 | 1.250
PR Open Time        |     0.667 | 0.667 | 0.875 | 1.000 | 1.000 | 1.250 | 1.250
Comment Frequency  |     0.500 | 0.500 | 0.750 | 0.800 | 0.800 | 1.000 | 1.000
Code Review Count  |     0.500 | 0.500 | 0.750 | 0.800 | 0.800 | 1.000 | 1.000

#### AHP Analysis Result

Metrics Name | Eigenvector | Weight
--- | --- | ---
Updated Issues Count|   1.380 | 19.721%
Close PR Count        | 1.380 | 19.721%
Issue First Response |  1.006 | 14.372%
Bug Issue Open Time |   0.901 | 12.876%
PR Open Time        |   0.901 | 12.876%
Comment Frequency  |    0.715 | 10.217%
Code Review Count  |    0.715 | 10.217%

#### Consistency Test Results

Largest Eigenvalue | CI Value | RI Value| CR Value | Consistency Test
--- | --- | --- | --- | ---
7.002 | 0.000 | 1.360 | 1.360 | PASS

### Threshold

The threshold we chose is based on the big-data observations from different types of open source projects.

## References

* [CHAOSS Metric Model: Community Service and Support](https://chaoss.community/kb/metrics-model-community-service-and-support/)

## Contributors

### Frontend

* Shengxiang Zhang
* Feng Zhong
* Chaoqun Huang
* Huatian Qin
* Xingyou Lai

### Backend

* Yehui Wang
* Chenqi Shan
* Shengbao Li
* Huatian Qin

### Metric Model

* Yehui Wang
* Liang Wang
* Chenqi Shan
* Shengbao Li
* Matt Germonprez
* Sean Goggins
