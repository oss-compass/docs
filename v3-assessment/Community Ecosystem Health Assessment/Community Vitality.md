# Community Vitality

Definition: Evaluating the community's activity level and attractiveness, reflecting the community's vitality and development potential.

# Assessment Model

**Community Popularity**

| Metric               | URL                                                                                                     | Threshold | Weight |
| -------------------- | ------------------------------------------------------------------------------------------------------- | --------- | ------ |
| Project Stars Growth | [/api/v3/community_popularity/stars](https://oss-compass.org/dataHub#api_v3_community_popularity_stars) | 100       | 0.50   |
| Project Forks Growth | [/api/v3/community_popularity/forks](https://oss-compass.org/dataHub#api_v3_community_popularity_forks) | 100       | 0.50   |

**Contribution Activity**

| Metric               | URL                                                                                                                                     | Threshold | Weight |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------- | ------ |
| Code Commit Count    | [/api/v3/contribution_activity/commit_count](https://oss-compass.org/dataHub#api_v3_contribution_activity_commit_count)                 | 12850     | 0.20   |
| Lines of Code Change | [/api/v3/contribution_activity/lines_of_code_change](https://oss-compass.org/dataHub#api_v3_contribution_activity_lines_of_code_change) | 300000    | 0.20   |
| PR Comment Count     | [/api/v3/contribution_activity/pr_comment_count](https://oss-compass.org/dataHub#api_v3_contribution_activity_pr_comment_count)         | 10        | 0.20   |
| New Issue Count      | [/api/v3/contribution_activity/new_issue_count](https://oss-compass.org/dataHub#api_v3_contribution_activity_new_issue_count)           | 10        | 0.20   |
| Issue Comment Count  | [/api/v3/contribution_activity/issue_comment_count](https://oss-compass.org/dataHub#api_v3_contribution_activity_issue_comment_count)   | 10        | 0.20   |

**Developer Base**

| Metric                     | URL                                                                                                                                   | Threshold | Weight |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------- | ------ |
| Community Contributor Count | [/api/v3/developer_base/contributor_count](https://oss-compass.org/dataHub#api_v3_developer_base_contributor_count)                   | 2000      | 0.33   |
| Code Contributor Count     | [/api/v3/developer_base/code_contributor_count](https://oss-compass.org/dataHub#api_v3_developer_base_code_contributor_count)         | 1000      | 0.33   |
| Non-Code Contributor Count | [/api/v3/developer_base/non_code_contributor_count](https://oss-compass.org/dataHub#api_v3_developer_base_non_code_contributor_count) | 500       | 0.17   |
| Community Follower Count  | [/api/v3/developer_base/follower_count](https://oss-compass.org/dataHub#api_v3_developer_base_follower_count)                         | 1000      | 0.17   |

# Metrics in Assessment Model

## Community Popularity

The community popularity model focuses on the project's visibility and attention in the developer community, reflecting the project's market influence.

### Project Stars Growth

- Definition: The number of new Stars added to the project during the statistical period, i.e., the difference between the cumulative total Stars in the current period and the cumulative total Stars in the previous period.
- Weight: 50%
- Threshold: 100

The number of Stars is an intuitive indicator of project popularity. This metric counts the number of new Stars added to the project during the statistical period, reflecting the project's attention and attractiveness in the developer community. Continuously growing Stars indicate that the project has good market influence and a user base.

### Project Forks Growth

- Definition: The number of new Forks added to the project during the statistical period, i.e., the difference between the cumulative total Forks in the current period and the cumulative total Forks in the previous period.
- Weight: 50%
- Threshold: 100

The number of Forks reflects developers' willingness to participate in the project. This metric counts the number of new Forks added to the project during the statistical period, indicating that developers are interested in the project and wish to conduct secondary development or contribute code based on the project. This is an important indicator for evaluating project activity and developer participation.

## Contribution Activity

The contribution activity model focuses on the frequency and scale of community contributions, reflecting the community's activity level.

### Code Commit Count

- Definition: The total number of new code commits (Commits) during the statistical period, deduplicated by commit hash.
- Weight: 20%
- Threshold: 12850

Code commit count is a core indicator of project development activity. This metric counts the total number of Commits submitted by community contributors during the statistical period. High-frequency code commits indicate that the project is in active development and community contributors are continuously engaged. This metric reflects the project's overall workload and development speed.

### Lines of Code Change

- Definition: The total volume of code line changes during the statistical period, including the sum of added and modified lines.
- Weight: 20%
- Threshold: 300000

Lines of code change reflects the scale of code contributions to the project. This metric counts the total volume of added and modified lines of code during the statistical period. Although lines of code cannot directly measure code quality, it can reflect the community's development investment level. Continuously growing lines of code indicate that the project is constantly evolving and improving.

### PR Comment Count

- Definition: The number of comments generated on PRs during the statistical period (excluding bot comments).
- Weight: 20%
- Threshold: 10

PR comment count reflects the community's code review activity. This metric counts the total number of comments on PRs during the statistical period. Active PR comments indicate that the community values code quality and collaborative development. This metric can reflect the community's collaboration atmosphere and technical exchange depth.

### New Issue Count

- Definition: The total number of new Issues created during the statistical period (excluding records that are PRs).
- Weight: 20%
- Threshold: 10

New Issue count reflects the community's problem feedback activity. This metric counts the total number of new Issues created by the community during the statistical period. This metric can reflect users' attention to the project and willingness to participate.

### Issue Comment Count

- Definition: The total number of comments under Issues during the statistical period (excluding bot comments).
- Weight: 20%
- Threshold: 10

Issue comment count reflects the community's problem discussion activity. This metric counts the total number of comments under Issues during the statistical period. Active Issue comments indicate that the community has a good communication atmosphere and problem-solving capability. This metric can reflect the community's collaboration efficiency and user support quality.

## Developer Base

The developer base model focuses on the scale of community contributors, reflecting the community's talent foundation.

### Community Contributor Count

- Definition: The total number of people participating in community contributions during the statistical period.
- Weight: 33%
- Threshold: 2000

Community contributor count is a core indicator of community scale. Contributors include code contributors and non-code contributors, reflecting the breadth of community participation. A large contributor base is an important guarantee for the community's sustainable development.

### Code Contributor Count

- Definition: The number of deduplicated users with code-related contribution behaviors such as code commits, PR merges, or PR comments during the statistical period.
- Weight: 33%
- Threshold: 1000

Code contributor count reflects the community's technical contribution capability. This metric counts the number of deduplicated users participating in code-related contributions during the statistical period. Contribution behaviors include the following types:

- Committer: The submitter who merges code commits (Commits) into the repository.

- PR Creator: Submits code changes by creating Pull Requests.

- PR Merger: Contributors who merge Pull Requests into the target branch.

- PR Commenter: Contributors who comment on the Pull Requests.

Code contributors are the core force driving the project's technical development. This metric can reflect the project's technical attractiveness and development activity.

### Non-Code Contributor Count

- Definition: The number of users who have made any contributions in the community during the statistical period, but have not engaged in code-related contributions.
- Weight: 17%
- Threshold: 500

The number of non-code contributors reflects the diversity of community participation. This metric counts contributors in the community who do not participate in direct code production activities—such as code commits and merges—but who contribute to the project's development through project maintenance, issue management, and community interaction. Based on the type of contribution, these contributors can be categorized into the following roles:

- Documentation Maintainers: Responsible for maintaining project-related textual information, including refining the descriptions of issues and pull requests and modifying title information.

- Issue Managers: Responsible for managing the lifecycle of issues, including creating issues, applying tags, tracking statuses, closing issues, and linking them to pull requests.

- Pull Request Collaboration Managers: Responsible for managing the pull request collaboration process, including task assignment, status maintenance, and tag management.

- Community Engagement Participants: Contribute to the project through lightweight community activities such as commenting on issues and participating in project discussions.

A large number of non-code contributors typically indicates a lower barrier to community participation, more diverse forms of contribution, and a more open and inclusive ecosystem.


### Community Follower Count

- Definition: The number of users who have starred or forked the project within the community during the statistical period.
- Weight: 17%
- Threshold: 1000

The number of community followers is a metric for measuring a project's community influence and external recognition. The number of users in the community who follow and share the project solely through stars or forks but do not participate in code commits, pull requests, issues, comments, or other forms of project collaboration reflects the community's reach and the potential scale of participation.

# Assessment Model Algorithm

## Weight

The weights of each metric are equally distributed.

### Community Popularity

2 metrics are equally distributed, with each metric having a weight of 50%.

### Contribution Activity

5 metrics are equally distributed, with each metric having a weight of 20%.

### Developer Base

4 metrics use differentiated weight allocation: Community Contributor Count and Code Contributor Count each account for 33%, while Non-Code Contributor Count and Community Follower Count each account for 17%.

## Threshold

The thresholds we selected are based on big data observations of different types of open source projects.
