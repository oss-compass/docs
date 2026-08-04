# Developer Growth

Definition: Evaluating the community's ability to cultivate developers from beginners to core contributors, reflecting the community's talent cultivation mechanism and growth path.

# Assessment Model

**Developer Participation Tiering**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| Organizational Code Core Contributors (including managers) | [/api/v3/participation_tier/org_code_core_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_org_code_core_contributors) | 10 | 0.08 |
| Organizational Issue Core Contributors (including managers) | [/api/v3/participation_tier/org_issue_core_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_org_issue_core_contributors) | 10 | 0.08 |
| Organizational Code Regular Contributors | [/api/v3/participation_tier/org_code_regular_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_org_code_regular_contributors) | 15 | 0.08 |
| Organizational Issue Regular Contributors | [/api/v3/participation_tier/org_issue_regular_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_org_issue_regular_contributors) | 15 | 0.08 |
| Organizational Code Visitor Contributors | [/api/v3/participation_tier/org_code_visitor_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_org_code_visitor_contributors) | 30 | 0.08 |
| Organizational Issue Visitor Contributors | [/api/v3/participation_tier/org_issue_visitor_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_org_issue_visitor_contributors) | 30 | 0.08 |
| Individual Code Core Contributors (including managers) | [/api/v3/participation_tier/individual_code_core_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_individual_code_core_contributors) | 20 | 0.08 |
| Individual Issue Core Contributors (including managers) | [/api/v3/participation_tier/individual_issue_core_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_individual_issue_core_contributors) | 20 | 0.08 |
| Individual Code Regular Contributors | [/api/v3/participation_tier/individual_code_regular_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_individual_code_regular_contributors) | 30 | 0.08 |
| Individual Issue Regular Contributors | [/api/v3/participation_tier/individual_issue_regular_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_individual_issue_regular_contributors) | 30 | 0.08 |
| Individual Code Visitor Contributors | [/api/v3/participation_tier/individual_code_visitor_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_individual_code_visitor_contributors) | 50 | 0.09 |
| Individual Issue Visitor Contributors | [/api/v3/participation_tier/individual_issue_visitor_contributors](https://oss-compass.org/dataHub#api_v3_participation_tier_individual_issue_visitor_contributors) | 50 | 0.09 |

**Developer Promotion**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| Organizational Code Core Promotion Count | [/api/v3/developer_promotion/org_code_core_promotion_count](https://oss-compass.org/dataHub#api_v3_developer_promotion_org_code_core_promotion_count) | 1 | 0.25 |
| Organizational Issue Core Promotion Count | [/api/v3/developer_promotion/org_issue_core_promotion_count](https://oss-compass.org/dataHub#api_v3_developer_promotion_org_issue_core_promotion_count) | 1 | 0.25 |
| Individual Code Core Promotion Count | [/api/v3/developer_promotion/individual_code_core_promotion_count](https://oss-compass.org/dataHub#api_v3_developer_promotion_individual_code_core_promotion_count) | 1 | 0.25 |
| Individual Issue Core Developer Promotion Count | [/api/v3/developer_promotion/individual_issue_core_promotion_count](https://oss-compass.org/dataHub#api_v3_developer_promotion_individual_issue_core_promotion_count) | 1 | 0.25 |

# Metrics in Assessment Model

## Developer Participation Tiering

The developer participation tiering model divides community contributors into three levels based on the cumulative proportion of contribution volume: core contributors (cumulative contribution volume ranking in the top 50%), regular contributors (cumulative ranking 50%–80%), and visitor contributors (cumulative ranking after 80%). This model is further subdivided along two dimensions—organization/individual and code/Issue—totalling 12 metrics. This tiering helps understand the community's talent structure, identify key contributors, and formulate targeted cultivation strategies.

### Organizational Code Core Contributors (including managers)

- Definition: The number of organizational contributors (including managers) whose cumulative code contribution volume ranks in the top 50% during the statistical period.
- Weight: 8%
- Threshold: 10

Organizational code core contributors are the primary decision-makers and implementers of the project's technical direction. This metric counts the number of organizational members whose cumulative code contribution volume accounts for the top 50% within the current period. They typically have deep project understanding and technical capabilities, responsible for core feature development and code review. This metric reflects the organization's deep participation in the project at the technical level.

### Organizational Issue Core Contributors (including managers)

- Definition: The number of organizational contributors (including managers) whose cumulative Issue activity ranks in the top 50% during the statistical period.
- Weight: 8%
- Threshold: 10

Organizational Issue core contributors play an important role in issue tracking, requirement management, and community communication. This metric counts the number of organizational members whose cumulative Issue activity accounts for the top 50% within the current period. They not only handle technical issues but also participate in community discussions and decisions. This metric reflects the organization's investment in community management and communication.

### Organizational Code Regular Contributors

- Definition: The number of organizational contributors whose cumulative code contribution volume ranks in the 50%–80% range during the statistical period.
- Weight: 8%
- Threshold: 15

Organizational code regular contributors are stable contributors to the project. This metric counts the number of organizational members whose cumulative code contribution volume accounts for the 50%–80% range within the current period. They regularly participate in code contributions, but their participation depth is not as deep as core contributors. They are the reserve force for core contributors and an important support for the community's sustainable development.

### Organizational Issue Regular Contributors

- Definition: The number of organizational contributors whose cumulative Issue activity ranks in the 50%–80% range during the statistical period.
- Weight: 8%
- Threshold: 15

Organizational Issue regular contributors regularly participate in Issue discussions and handling. This metric counts the number of organizational members whose cumulative Issue activity accounts for the 50%–80% range within the current period. They provide continuous problem feedback and solutions for the community, ensuring timely response and handling of community issues.

### Organizational Code Visitor Contributors

- Definition: The number of organizational contributors whose cumulative code contribution volume ranks after 80% during the statistical period.
- Weight: 8%
- Threshold: 30

Organizational code visitor contributors are developers who occasionally participate in code contributions. This metric counts the number of organizational members whose cumulative code contribution volume accounts for the tail after 80% within the current period. They may be first-time contributors or temporary participants. This metric reflects the community's attractiveness and inclusiveness to new contributors.

### Organizational Issue Visitor Contributors

- Definition: The number of organizational contributors whose cumulative Issue activity ranks after 80% during the statistical period.
- Weight: 8%
- Threshold: 30

Organizational Issue visitor contributors occasionally participate in Issue discussions and feedback. This metric counts the number of organizational members whose cumulative Issue activity accounts for the tail after 80% within the current period. Although their participation is not frequent, it brings diverse perspectives and feedback to the community.

### Individual Code Core Contributors (including managers)

- Definition: The number of individual contributors (including managers) whose cumulative code contribution volume ranks in the top 50% during the statistical period.
- Weight: 8%
- Threshold: 20

Individual code core contributors are the backbone of independent contributors. This metric counts the number of individual developers whose cumulative code contribution volume accounts for the top 50% within the current period. They do not rely on organizational support but make continuous contributions to the project based on personal passion and professional capabilities. This metric reflects the community's attractiveness and cultivation ability for individual contributors.

### Individual Issue Core Contributors (including managers)

- Definition: The number of individual contributors (including managers) whose cumulative Issue activity ranks in the top 50% during the statistical period.
- Weight: 8%
- Threshold: 20

Individual Issue core contributors play an important role in community communication and issue management. This metric counts the number of individual developers whose cumulative Issue activity accounts for the top 50% within the current period. Their continuous participation ensures timely response and effective resolution of community issues.

### Individual Code Regular Contributors

- Definition: The number of individual contributors whose cumulative code contribution volume ranks in the 50%–80% range during the statistical period.
- Weight: 8%
- Threshold: 30

Individual code regular contributors are stable contributors to the project. This metric counts the number of individual developers whose cumulative code contribution volume accounts for the 50%–80% range within the current period. They regularly participate in code contributions and are an important force for the community's sustainable development, as well as potential candidates for core contributors.

### Individual Issue Regular Contributors

- Definition: The number of individual contributors whose cumulative Issue activity ranks in the 50%–80% range during the statistical period.
- Weight: 8%
- Threshold: 30

Individual Issue regular contributors regularly participate in Issue discussions and handling. This metric counts the number of individual developers whose cumulative Issue activity accounts for the 50%–80% range within the current period. They provide continuous problem feedback and solutions for the community.

### Individual Code Visitor Contributors

- Definition: The number of individual contributors whose cumulative code contribution volume ranks after 80% during the statistical period.
- Weight: 9%
- Threshold: 50

Individual code visitor contributors are developers who occasionally participate in code contributions. This metric counts the number of individual developers whose cumulative code contribution volume accounts for the tail after 80% within the current period. They may be first-time contributors or temporary participants. This metric reflects the community's attractiveness and inclusiveness to new contributors.

### Individual Issue Visitor Contributors

- Definition: The number of individual contributors whose cumulative Issue activity ranks after 80% during the statistical period.
- Weight: 9%
- Threshold: 50

Individual Issue visitor contributors occasionally participate in Issue discussions and feedback. This metric counts the number of individual developers whose cumulative Issue activity accounts for the tail after 80% within the current period. Their participation brings diverse perspectives and feedback to the community.

## Developer Promotion

The developer promotion model focuses on the situation of developers being promoted from lower levels to higher levels, reflecting the community's talent cultivation effectiveness.

### Organizational Code Core Promotion Count

- Definition: The number of organizational members promoted from non-core to code core contributors or managers during the statistical period.
- Weight: 25%
- Threshold: 1

The organizational code core promotion count reflects the organization's ability to cultivate developers. This metric counts the number of organizational members who grew from non-core in the previous period to core code contributors in the current period, plus the number of organizational members promoted to managers in the current period. A successful promotion mechanism can motivate developers to continue contributing and enhance the project's technical strength.

### Organizational Issue Core Promotion Count

- Definition: The number of organizational members promoted from non-core to Issue core contributors or managers during the statistical period.
- Weight: 25%
- Threshold: 1

The organizational Issue core promotion count reflects the organization's effectiveness in cultivating community management and communication talents. This metric counts the number of organizational members who grew from non-core in the previous period to core Issue contributors in the current period, plus the number of organizational members promoted to managers in the current period. These promoted developers play an important role in community governance.

### Individual Code Core Promotion Count

- Definition: The number of individual developers promoted from non-core to code core contributors or managers during the statistical period.
- Weight: 25%
- Threshold: 1

The individual code core promotion count reflects the community's ability to cultivate individual contributors. This metric counts the number of individual developers who grew from non-core in the previous period to core code contributors in the current period, plus the number of individual developers promoted to managers in the current period. A successful promotion mechanism can motivate individual developers to continue contributing and enhance community vitality.

### Individual Issue Core Developer Promotion Count

- Definition: The number of individual developers promoted from non-core to Issue core contributors or managers during the statistical period.
- Weight: 25%
- Threshold: 1

The individual Issue core developer promotion count reflects the community's effectiveness in cultivating community management and communication talents. This metric counts the number of individual developers who grew from non-core in the previous period to core Issue contributors in the current period, plus the number of individual developers promoted to managers in the current period.

# Assessment Model Algorithm

## Weight

The weights of each metric are equally distributed.

### Developer Participation Tiering

12 metrics are equally distributed, with each metric having a weight of approximately 8.33%.

### Developer Promotion

4 metrics are equally distributed, with each metric having a weight of 25%.

## Threshold

The thresholds we selected are based on big data observations of different types of open source projects.
