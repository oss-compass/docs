# Collaboration Efficiency

Definition: Evaluating the community's collaboration quality and response efficiency, reflecting the community's collaboration maturity and service level.

# Assessment Model

**Response Timeliness**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| Issue Unresponsive Rate | [/api/v3/response_timeliness/issue_unresponsive_rate](https://oss-compass.org/dataHub#api_v3_response_timeliness_issue_unresponsive_rate) | 1 ratio | 0.17 |
| Issue First Response Time | [/api/v3/response_timeliness/issue_first_reponse](https://oss-compass.org/dataHub#api_v3_response_timeliness_issue_first_reponse) | 15 days | 0.17 |
| Issue Processing Time | [/api/v3/response_timeliness/issue_open_time](https://oss-compass.org/dataHub#api_v3_response_timeliness_issue_open_time) | 60 days | 0.17 |
| PR Unresponsive Rate | [/api/v3/response_timeliness/pr_unresponsive_rate](https://oss-compass.org/dataHub#api_v3_response_timeliness_pr_unresponsive_rate) | 1 ratio | 0.17 |
| PR First Response Time | [/api/v3/response_timeliness/pr_time_to_first_response](https://oss-compass.org/dataHub#api_v3_response_timeliness_pr_time_to_first_response) | 15 days | 0.17 |
| PR Processing Time | [/api/v3/response_timeliness/pr_open_time](https://oss-compass.org/dataHub#api_v3_response_timeliness_pr_open_time) | 30 days | 0.17 |

**Collaboration Development Quality**

| Metric | URL                                                                                                                                                     | Threshold | Weight |
| ------ |---------------------------------------------------------------------------------------------------------------------------------------------------------| --------- | ------ |
| PR Code Submission Rate | [/api/v3/collaboration_quality/pr_commit_rate](https://oss-compass.org/dataHub#api_v3_collaboration_quality_pr_commit_rate)                              | 1 | 0.17 |
| PR/Issue Link Rate | [/api/v3/collaboration_quality/pr_issue_link_rate](https://oss-compass.org/dataHub#api_v3_collaboration_quality_pr_issue_link_rate)                     | 1 ratio | 0.17 |
| PR Review Participation Rate | [/api/v3/collaboration_quality/pr_review_participation_rate](https://oss-compass.org/dataHub#api_v3_collaboration_quality_pr_review_participation_rate) | 1 ratio | 0.17 |
| Merge Collaboration Rate | [/api/v3/collaboration_quality/pr_non_author_merge_rate](https://oss-compass.org/dataHub#api_v3_collaboration_quality_pr_non_author_merge_rate)         | 1 ratio | 0.17 |
| PR Average Interactions | [/api/v3/collaboration_quality/pr_average_interactions](https://oss-compass.org/dataHub#api_v3_collaboration_quality_pr_average_interactions)           | 1 | 0.17 |
| Tiered Code Review Time | [/api/v3/collaboration_quality/pr_review_time_by_size](https://oss-compass.org/dataHub#api_v3_collaboration_quality_pr_review_time_by_size)             | 10 days | 0.17 |

# Metrics in Assessment Model

## Response Timeliness

The response timeliness model focuses on the community's response speed to Issues and PRs, reflecting the community's service level and communication efficiency.

### Issue Unresponsive Rate

- Definition: The proportion of new Issues that did not receive any response to the total number of Issues during the statistical period.
- Weight: 17%
- Threshold: 1 ratio (100%)

The Issue unresponsive rate reflects the community's attention to user problems. This metric counts the proportion of new Issues that had not received any comments and were still in the open state by the end of the period. Unresponsive Issues make users feel ignored, affecting user experience and community reputation. Reducing the unresponsive rate is an important goal for improving community service quality.

### Issue First Response Time

- Definition: The average time for new Issues to receive their first response during the statistical period.
- Weight: 17%
- Threshold: 15 days

Issue first response time is a key indicator of community response speed. This metric counts the time from creation to the first non-bot comment for new Issues during the statistical period. A quick first response can bring a good experience to users and enhance their trust in the community. This metric reflects the community's communication efficiency and service awareness.

### Issue Processing Time

- Definition: The average time for Issues from creation to closure during the statistical period.
- Weight: 17%
- Threshold: 60 days

Issue processing time reflects the community's efficiency in solving problems. This metric counts the processing time of new Issues during the statistical period: for closed Issues, the difference between the closure time and the creation time is taken; for unclosed Issues, the difference between the period cutoff (statistical moment) and the creation time is taken. A shorter processing time indicates that the community can quickly solve user problems and improve user satisfaction.

### PR Unresponsive Rate

- Definition: The proportion of new PRs that did not receive any response to the total number of new PRs during the statistical period.
- Weight: 17%
- Threshold: 1 ratio (100%)

The PR unresponsive rate reflects the community's attention to code contributions. This metric counts the proportion of new PRs that were neither merged nor received any non-bot comments by the end of the period. Unresponsive PRs can make contributors feel frustrated, affecting contributor enthusiasm and retention. Reducing the PR unresponsive rate is an important measure for maintaining good contributor relationships.

### PR First Response Time

- Definition: The average time for new PRs to receive their first response during the statistical period.
- Weight: 17%
- Threshold: 15 days

PR first response time is a key indicator of the community's response speed to code contributions. This metric counts the time from creation to the first non-bot comment for new PRs during the statistical period (average value, in days). A quick first response can bring a good experience to contributors and enhance their trust in the community. This metric reflects the community's collaboration efficiency and contributor support quality.

### PR Processing Time

- Definition: The average processing time for PRs from creation to merge or closure during the statistical period.
- Weight: 17%
- Threshold: 30 days

PR processing time reflects the community's efficiency in handling code contributions. This metric counts the processing time of new PRs during the statistical period: for merged or closed PRs, the difference between the end time and the creation time is taken; for unfinished PRs, the difference between the period cutoff (statistical moment) and the creation time is taken (average value, in days). A shorter processing time can reduce contributor waiting time and lower the risk of merge conflicts. This metric is an important indicator for evaluating community collaboration efficiency.

## Collaboration Development Quality

The collaboration development quality model focuses on the community's code review and collaboration process quality, reflecting the community's development maturity.

### PR Code Submission Rate

- Definition: The proportion of commits generated by successfully merged PRs to the total commits during the statistical period.
- Weight: 17%
- Threshold: 1 (100%)

The PR code submission rate reflects how standardized the community is in submitting code through the PR process. This metric counts the proportion of commits generated by successfully merged PRs to the total project commits during the statistical period. A higher proportion indicates that the project's code is mainly merged through the PR process and that code changes are reviewed, which helps ensure code quality. This metric can reflect the community's collaboration standardization and code review coverage.

### PR/Issue Link Rate

- Definition: The proportion of PRs linked to Issues to the total number of PRs during the statistical period.
- Weight: 17%
- Threshold: 1 ratio (100%)

The PR/Issue link rate reflects the community's collaboration standardization. This metric counts the proportion of PRs linked to Issues among all PRs during the statistical period. Linking Issues can help understand the background and purpose of code changes, improving code review efficiency. This metric reflects the community's collaboration maturity and process standardization.

### PR Review Participation Rate

- Definition: The proportion of reviewed PRs to the total number of PRs during the statistical period.
- Weight: 17%
- Threshold: 1 ratio (100%)

The PR review participation rate reflects the community's code review culture. This metric counts the proportion of new PRs with non-author review records (review comments or assignee acceptance) during the statistical period. Reviewed PRs can ensure code quality and reduce defects and security risks. This metric reflects the community's emphasis on code quality.

### Merge Collaboration Rate

- Definition: The proportion of PRs merged by non-authors to the total number of merged PRs during the statistical period.
- Weight: 17%
- Threshold: 1 ratio (100%)

The merge collaboration rate reflects the community's collaboration security. This metric counts the proportion of PRs whose merger is not the same person as the author to the total number of merged PRs during the statistical period. Having non-authors merge PRs can prevent permission abuse and ensure the effectiveness of code review. This metric reflects the community's governance maturity and security awareness.

### PR Average Interactions

- Definition: The average number of comment interactions per PR during the statistical period.
- Weight: 17%
- Threshold: 1

PR average interactions reflect the community's collaboration depth. This metric counts the ratio of the total number of comments on new PRs to the number of new PRs during the statistical period (excluding bot comments). More interactions indicate that the community has fully discussed and reviewed code changes, helping to improve code quality. This metric can reflect the community's collaboration atmosphere and technical exchange depth.

### Tiered Code Review Time

- Definition: The average review time for PRs tiered by code change size during the statistical period.
- Weight: 17%
- Threshold: 10 days

Tiered code review time reflects the community's review efficiency. This metric counts the average first review response time for PRs at each tier, based on the number of code changed lines. Tiered review based on PR size can optimize review resource allocation and improve review efficiency. This metric reflects the maturity of the community's review process.

# Assessment Model Algorithm

## Weight

The weights of each metric are equally distributed.

### Response Timeliness

6 metrics are equally distributed, with each metric having a weight of approximately 16.67%.

### Collaboration Development Quality

6 metrics are equally distributed, with each metric having a weight of approximately 16.67%.

## Threshold

The thresholds we selected are based on big data observations of different types of open source projects.
