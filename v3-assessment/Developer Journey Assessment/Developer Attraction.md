# Developer Attraction

Definition: Evaluating the community's ability to attract new developers to join, reflecting the community's attractiveness and newcomer-friendliness.

# Assessment Model

**Developer Attraction**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| New Organizations | [/api/v3/developer_attraction/new_org_count](https://oss-compass.org/dataHub#api_v3_developer_attraction_new_org_count) | 10 | 0.20 |
| New Organizational Code Contributors | [/api/v3/developer_attraction/new_org_code_contributors](https://oss-compass.org/dataHub#api_v3_developer_attraction_new_org_code_contributors) | 20 | 0.20 |
| New Organizational Non-Code Contributors | [/api/v3/developer_attraction/new_org_non_code_contributors](https://oss-compass.org/dataHub#api_v3_developer_attraction_new_org_non_code_contributors) | 20 | 0.20 |
| New Individual Code Contributors | [/api/v3/developer_attraction/new_individual_code_contributors](https://oss-compass.org/dataHub#api_v3_developer_attraction_new_individual_code_contributors) | 30 | 0.20 |
| New Individual Non-Code Contributors | [/api/v3/developer_attraction/new_individual_non_code_contributors](https://oss-compass.org/dataHub#api_v3_developer_attraction_new_individual_non_code_contributors) | 30 | 0.20 |

# Metrics in Assessment Model

## New Organizations

- Definition: The number of organizations that contributed to the community for the first time during the statistical period.
- Weight: 20%
- Threshold: 10

Organizational participation is an important indicator of open source community maturity. This metric counts the deduplicated number of organizations that made effective contributions for the first time within the current period, i.e., the difference between the active organizations in the current period and all organizations that have participated in all historical periods. The number of new organizations reflects the community's attractiveness to enterprises, research institutions, and other organizations. The addition of organizations not only brings more resource investment but also enhances the project's sustainable development capability. This metric helps us understand the expansion speed of the community at the organizational level.

## New Organizational Code Contributors

- Definition: The number of organizational members who made code contributions for the first time during the statistical period.
- Weight: 20%
- Threshold: 20

Organizational code contributors are the core force driving project technical development. This metric counts the number of organizational members who made code contributions for the first time within the current period, i.e., the difference between the active organizational code contributors in the current period and the organizational code contributors across all historical periods. The number of new organizational code contributors reflects the organization's investment level and willingness to participate in the project. These developers typically have professional technical backgrounds and resource support, and their addition can significantly enhance the project's technical strength and code quality.

## New Organizational Non-Code Contributors

- Definition: The number of organizational members who made non-code contributions for the first time during the statistical period.
- Weight: 20%
- Threshold: 20

Non-code contributions include documentation writing, community management, and various other forms. This metric counts the number of organizational members who made non-code contributions for the first time within the current period, i.e., the difference between the active organizational non-code contributors in the current period and the organizational non-code contributors across all historical periods. The number of new organizational non-code contributors reflects the organization's comprehensive support for the project. Although non-code contributors do not directly participate in code development, they play an important role in documentation improvement, user experience enhancement, and community building.

## New Individual Code Contributors

- Definition: The number of individual developers who made code contributions for the first time during the statistical period.
- Weight: 20%
- Threshold: 30

Individual code contributors are the foundational force of open source communities. This metric counts the number of individual developers who made code contributions for the first time within the current period, i.e., the difference between the active individual code contributors in the current period and the individual code contributors across all historical periods. The number of new individual code contributors reflects the community's attractiveness to independent developers. These developers may come from different backgrounds, and their diverse perspectives and contributions can enrich the project's technical ecosystem. Maintaining a continuous inflow of individual developers is an important guarantee for community vitality.

## New Individual Non-Code Contributors

- Definition: The number of individual developers who made non-code contributions for the first time during the statistical period.
- Weight: 20%
- Threshold: 30

Individual non-code contributors are an important component of community diversity. This metric counts the number of individual developers who made non-code contributions for the first time within the current period, i.e., the difference between the active individual non-code contributors in the current period and the individual non-code contributors across all historical periods. The number of new individual non-code contributors reflects the community's inclusiveness towards different types of contributors. These contributors may participate in translation, documentation improvement, community event organization, and other work. Their participation lowers the contribution threshold and expands the community's participation scope.

# Assessment Model Algorithm

## Weight

The weights of each metric are equally distributed, with each metric having a weight of 20%.

## Threshold

The thresholds we selected are based on big data observations of different types of open source projects.
