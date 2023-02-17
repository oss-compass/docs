---
title: Collaboration Development Index
slug: /metrics-models/productivity/collaboration-development-index
tags:
  - Metrics Models
  - Productivity
  - Collaboration Development Index
description: Use proxy metrics to evaluate how well the development process is managed and how well the community is doing with collaborative development
---

# Collaboration Development Index

Open source projects, as a typical manifestation of human group intelligence, the ability to establish collaborative development management is a key element contributing to the success of the project. And code, as the final output of a project, is the essence of the entire community's contribution. So we evaluate how well the development process is managed and how well the community does collaborative development around a series of indirect metrics related to code contribution.

# Metrics in the Metrics Model

## Code Contributor Count

* Definition: Determine how many active pr creators, code reviewers, commit authors there are in the past 90 days.
* Weight: 19.987%
* Threshold: 1000

Here we focus on the number of contributors directly related to the code contribution. As a result of this model, it identifies a well-managed community of development collaborations that are gathering more and more active code contributors. We believe that some types of the Issue are also related to code contributions, such as Bug , new requirements, and so on, and will eventually introduce code contributions. But as a general indicator, it is difficult to identify issues in a uniform way (such as a Bug type) within the specific type of each project, because each project has a different definition and understanding of the Bug type. So we made a trade-off, choosing only PR-related and Code Commit-related contributors as insight objects.

## Commit Frequency

* Definition: Determine the average number of commits per week in the past 90 days.
* Weight: 16.363%
* Threshold: 1000

As an outcome indicator of this model, it identifies the sustainability and quantity of project contributions. Refers to the overall workload of the project.

## Is Maintained

* Definition: Percentage of weeks with at least one code commit in the past 90 days(single repository). Percentage of code repositories with at least one code commit in the last 30 days(multiple repositories).
* Weight: 13.853%
* Threshold: 100%
* Note: definitions of single repository and multiple repositories are differerent. 

This metric is used to determine whether the repository is being maintained on an ongoing basis. An actively maintained projects may be more resistant to risks such as vulnerabilities. It is related to the [Commit Frequency](#commit-frequency), but the focus is different. The former focuses on the number of code contributions during the cycle, while the latter focuses on the continuity of the code contributions. But we should not draw any direct conclusions about projects that are low on this indicator, and further insights are needed.

## Commit PR Linked Ratio

* Definition: Determine the percentage of new code commit link pull request in the last 90 days. 
* Weight: 12.612%
* Threshold: 100%

This indicator is used to determine whether the code submission has gone through the PR process. To determine whether a project is open source, perhaps we can verify the License it declares. But whether open source projects use open community collaboration model to develop, and whether the community is willing to build community with open source contributors and organizational partners, it is not enough to rely on License alone. Here we examine the project's willingness to collaborate by informing contributors in an open and transparent manner about the purpose of the code submission, whether it is a PR or not, and by being reviewed.

## PR Issue Linked Ratio

* Definition: Determine the percentage of new pull request link issues in the last 90 days. 
* Weight: 11.319%
* Threshold: 100%

This metric is used to see if the code contributions are based upon open discussion, for example using the Issue. Note that not all issues result in code contributions, such as an Issue for the advisory type, there would be no code modifications generally . At the same time, we should also note that if PR goes through public discussion, Issue is not the only way, it may come from discussion in the forum. Therefore, we can not blindly pursue the high proportion of this indicator.

## Code Review Ratio

* Definition: Determine the percentage of code commits with at least one reviewer (not PR creator) in the last 90 days. 
* Weight: 10.113%
* Threshold: 100%

If a PR is merged without being reviewed by others, the probability of a code defect or vulnerability being introduced, intentionally or unintentionally, is greatly increased. Code reviews do not fully protect against this risk, but they greatly improve the introduction of risk.

## Code Merge Ratio

* Definition: Determine the percentage of PR Mergers and PR authors who are not the same person in the last 90 days of commits. 
* Weight: 10.113%
* Threshold: 100%

This metric was observed in conjunction with the [Code Review Ratio](code-review-ratio). When we introduced a third-party review, but if the PR creator intentionally or unintentionally ignored the third-party review and merged the code directly, there are also risks. It's important to note that the [Code Review Ratio](code-review-ratio) and [Code Merge Ratio](code-merge-ratio) are one best practices we observe in opensource communities, but rather the only standards. We also see in some communities based on trust in some good, long-term contributors, these people are granted the right to merge their own code direclty.

## Lines of Code Frequency

* Definition: Determine the average number of lines touched (lines added plus lines removed) per week in the past 90 days. 
* Weight: 5.640%
* Threshold: 300000

The number of lines of source code is indeed strongly correlated with the amount of work, but it is less correlated with the value created. What forms of code can be counted in the LOC, are uncertain factors. We do not care so much about the code form(program language, configuration files etc), only use it as the description of the workload, so its weight in the overall metrics model is low.

# Metric Model Algorithm

## Weight

We use [AHP](https://en.wikipedia.org/wiki/Analytic_hierarchy_process) to calculate weight of each metric.

### AHP Input Data

Metric Name | Code Contributor Count | Commit Frequency | Is Maintained | Commit PR Linked Ratio | PR Issue Linked Ratio | Code Review Ratio | Code Merge Ratio | Lines of Code Frequency
--- | --- | --- | --- | --- | --- | --- | --- | --- 
Code Contributor Count |  1.000 | 1.111	| 1.250	| 1.429	| 1.667	| 2.000	| 2.000	| 5.000
Commit Frequency |  0.900 | 1.000	| 1.250	| 1.250	| 1.429	| 1.667	| 1.667	| 2.500
Is Maintained |  0.800 | 0.800	| 1.000	| 1.111	| 1.250	| 1.429	| 1.429	| 2.000
Commit PR Linked Ratio |  0.700 | 0.800	| 0.900	| 1.000	| 1.111	| 1.250	| 1.250	| 2.000
PR Issue Linked Ratio |  0.600 | 0.700	| 0.800	| 0.900	| 1.000	| 1.111	| 1.111	| 2.000
Code Review Ratio |  0.500 | 0.600	| 0.700	| 0.800	| 0.900	| 1.000	| 1.000	| 2.000
Code Merge Ratio |  0.500 | 0.600	| 0.700	| 0.800	| 0.900	| 1.000	| 1.000	| 2.000
Lines of Code Frequency | 0.200 | 0.400	| 0.500	| 0.500	| 0.500	| 0.500	| 0.500	| 1.000

### AHP Analysis Result

Metrics Name | Eigenvector | Weight
--- | --- | ---
Contributor Count |  1.599	| 19.987%	
Commit Frequency |  1.309	| 16.363%
Is Maintained |  1.108	| 13.853%
Commit PR Linked Ratio |  1.009	| 12.612%
PR Issue Linked Ratio |  0.906	| 11.319%
Code Review Ratio |  0.809	| 10.113%
Code Merge Ratio |  0.809	| 10.113%
Lines of Code Frequency | 0.451	| 5.640%

### Consistency Test Results

Largest Eigenvalue | CI Value | RI Value| CR Value | Consistency Test
--- | --- | --- | --- | ---
8.034 | 0.005 | 1.410 | 0.003 | PASS

## Threshold

The threshold we chose is based on the big-data observations from different types of open source projects.

# References

* [CHAOSS Metric Model: Collaboration Development Index](https://chaoss.community/kb/metrics-model-collaboration-development-index/)

# Contributors
## Frontend
* Shengxiang Zhang
* Feng Zhong
* Chaoqun Huang
* Huatian Qin
* Xingyou Lai

## Backend
* Yehui Wang
* Chenqi Shan
* Shengbao Li
* Huatian Qin

## Metric Model
* Yehui Wang
* Liang Wang
* Chenqi Shan 
* Matt Germonprez
* Sean Goggins
* Vinod Ahuja