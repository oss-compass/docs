---
title: Contributor Domain Persona
slug: /metrics-models/people/productivity/contributor-domain-persona
tags:
  - Metrics Models
  - people
  - Productivity
  - Contributor Domain Persona
---

# Contributor Domain Persona

In the Domain Persona Model, we first categorize the contributions made by contributors to the community by domain or type. We strive to atomize the contribution domains more finely, matching our current engineering capabilities. However, this categorization process is an ongoing evolution, and as our engineering capabilities improve, we will be able to achieve more granular domain divisions.

For observation-type contributions, issue-type contributions, and code-type contributions, we can use insights provided by code hosting platforms (such as GitHub, Gitee, etc.). For other types of contributions, due to differences in community usage and extent, currently we can only provide limited data sources as references. However, as our engineering capabilities gradually improve, we may provide more solutions.

![image](https://github.com/oss-compass/docs/assets/53640896/e83a67f0-acdc-4251-b3c9-5fbba4a0a422)

- Observation-type contributions: Contributors express interest and attention to a project through actions like star, fork, and watch, which can enhance and showcase the project's level of attention but do not directly contribute to the project.
- Issue-type contributions: Contributions related to issues can be categorized based on the type of issues, such as usage inquiries, bug reports, task planning, etc. However, we currently lack a universal solution to identify issue types. Therefore, we classify contributions into two types based on contributor behavior in issues: regular contributions and management contributions.
  - Regular Issue contributions: Issue creation and comments.
  - Management Issue contributions: Eight types of management actions, including labeling, closing, reopening, assigning responsibility, marking as duplicate, migrating, milestones, and locking comments. While these contributions are often overlooked, they are crucial for community managers to ensure smooth issue handling, and thus, we should include them in the observation scope.
- Code-type contributions: Similar to Issue-type contributions, we categorize code contributions into regular and management contributions:
  - Regular Code contributions: Code development, Pull Request creation, and Code Review.
  - Management Code contributions: Code direct submissions, along with ten types of Pull Request management actions, including labeling, closing, reopening, assigning responsibility, marking as duplicate, migrating, milestones, locking comments, merging, and reviewing, and so on. Similar to Issue management contributions, these management actions require significant effort from community managers to ensure smooth code integration.
- Forum-type contributions: If an open source community builds forum services based on frameworks that provide publicly accessible data channels, such as Discourse, we can observe contributions to the forum, such as creating topics and comments.
- Chat platform-type contributions: We support data inspection methods based on chat platforms like Slack, Discord, etc.
- Media platform-type contributions: Currently, our data mainly comes from Twitter.
- Event-type contributions: Our data currently depends on manual input, including online and offline events.
- Sponsor: Cash donations.

# Metrics in the Metrics Model

## Code Contributor Count

- Definition: How many active code class contributors in the last 90 days.
- Weight: 16%
- Threshold: 500

## Code Contribution Count

- Definition: The number of contributions per capita for contributors in the active code class in the last 90 days.
- Weight: 24%
- Threshold: 15

## Issue Contributor Count

- Definition: How many active issue class contributors in the last 90 days.
- Weight: 16%
- Threshold: 1000

## Issue Contribution Count

- Definition: The number of contributions per capita for contributors in the active issue class in the last 90 days.
- Weight: 24%
- Threshold: 10

## Observation Contributor Count

- Definition: How many active observation class contributors in the last 90 days.
- Weight: 8%
- Threshold: 2000

## Observation Contribution Count

- Definition: The number of contributions per capita for contributors in the active observation class in the last 90 days.
- Weight: 12%
- Threshold: 2

# Metric Model Algorithm

## Weight

We use [AHP](https://en.wikipedia.org/wiki/Analytic_hierarchy_process) to calculate weight of each metric.

### AHP Input Data

| Metric Name                    | Code Contributor Count | Code Contribution Count | Issue Contributor Count | Issue Contribution Count | Observation Contributor Count | Observation Contribution Count |
| ------------------------------ | ---------------------- | ----------------------- | ----------------------- | ------------------------ | ----------------------------- | ------------------------------ | ----- |
| Code Contributor Count         | 1.000                  | 0.667                   | 1.000                   | 0.667                    | 2.000                         | 1.333                          |
| Code Contribution Count        | 1.500                  | 1.000                   | 1.500                   | 1.000                    | 3.000                         | 2.000                          |
| Issue Contributor Count        | 1.000                  | 0.667                   | 1.000                   | 0.667                    | 2.000                         | 1.333                          |
| Issue Contribution Count       | 1.500                  | 1.000                   | 1.500                   | 1.000                    | 3.000                         | 2.000                          |
| Observation Contributor Count  | 0.800                  | 0.500                   | 0.333                   | 0.500                    | 0.333                         | 1.000                          | 0.667 |
| Observation Contribution Count | 0.750                  | 0.500                   | 0.750                   | 0.500                    | 1.500                         | 1.000                          |

### AHP Analysis Result

| Metrics Name                   | Eigenvector | Weight  |
| ------------------------------ | ----------- | ------- |
| Code Contributor Count         | 0.960       | 16.000% |
| Code Contribution Count        | 1.440       | 24.000% |
| Issue Contributor Count        | 0.960       | 16.000% |
| Issue Contribution Count       | 1.440       | 24.000% |
| Observation Contributor Count  | 0.480       | 8.000%  |
| Observation Contribution Count | 0.720       | 12.000% |

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
