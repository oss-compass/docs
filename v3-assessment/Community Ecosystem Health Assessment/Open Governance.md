# Open Governance

Definition: Evaluating the community's governance openness and inclusiveness, reflecting the community's governance maturity and diversity level.

# Assessment Model

**Organizational Open Governance**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| Number of Organizations Participating in Governance | [/api/v3/organizational_governance/governance_orgs_by_period](https://oss-compass.org/dataHub#api_v3_organizational_governance_governance_orgs_by_period) | 5 | 0.33 |
| Number of Organizational Managers | [/api/v3/organizational_governance/org_managers_by_period](https://oss-compass.org/dataHub#api_v3_organizational_governance_org_managers_by_period) | 20 | 0.33 |
| Organizational Manager Ratio | [/api/v3/organizational_governance/org_managers_ratio_by_period](https://oss-compass.org/dataHub#api_v3_organizational_governance_org_managers_ratio_by_period) | 1 ratio | 0.33 |

**Individual Open Governance**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| Number of Individual Managers | [/api/v3/personal_governance/individual_managers_by_period](https://oss-compass.org/dataHub#api_v3_personal_governance_individual_managers_by_period) | 10 | 0.5 |
| Individual Manager Ratio | [/api/v3/personal_governance/individual_managers_ratio_by_period](https://oss-compass.org/dataHub#api_v3_personal_governance_individual_managers_ratio_by_period) | 1 ratio | 0.5 |

# Metrics in Assessment Model

## Organizational Open Governance

The organizational open governance model focuses on the participation of organizations in community governance, reflecting the community's organizational diversity and governance openness.

### Number of Organizations Participating in Governance

- Definition: The number of external organizations participating in community governance during the statistical period.
- Weight: 33%
- Threshold: 5

The number of organizations participating in governance reflects the community's organizational diversity level. This metric counts the number of users in the community who serve as organization managers or organization participants during the statistical period. Multiple organizations participating in governance can avoid single organization monopoly in decision-making, ensuring the community's neutrality and sustainable development. This metric is an important indicator for evaluating community open governance.

### Number of Organizational Managers

- Definition: The number of managers from external organizations during the statistical period.
- Weight: 33%
- Threshold: 20

The number of organizational managers reflects the organization's investment in community governance. This metric counts the number of users in the community who serve as organization managers during the statistical period. Organizational managers typically have rich project experience and resource support, and their participation can enhance the professionalism and efficiency of community governance. This metric can reflect the organization's emphasis on community governance.

### Organizational Manager Ratio

- Definition: The proportion of organizational managers to the total number of community managers during the statistical period.
- Weight: 33%
- Threshold: 1 ratio (100%)

The organizational manager ratio reflects the organization's influence in community governance. This metric counts the proportion of managers from organizations to all community managers (the sum of organizational managers and individual managers) during the statistical period. An appropriate organizational manager ratio can ensure the community's professionalism and resource support, but an excessively high ratio may lead to excessive dependence on organizations in community governance, affecting the community's independence and neutrality.

## Individual Open Governance

The individual open governance model focuses on the participation of individuals in community governance, reflecting the community's individual participation level and governance inclusiveness.

### Number of Individual Managers

- Definition: The number of managers from individuals during the statistical period.
- Weight: 50%
- Threshold: 10

The number of individual managers reflects the community's recognition and cultivation of individual contributors. This metric counts the number of deduplicated users who serve as individual managers in the community during the statistical period. Individual managers typically gain governance rights through personal ability and contributions, and their participation can ensure the community's diversity and vitality. This metric can reflect the community's individual participation level and governance inclusiveness.

### Individual Manager Ratio

- Definition: The proportion of individual managers to the total number of community managers during the statistical period.
- Weight: 50%
- Threshold: 1 ratio (100%)

The individual manager ratio reflects the influence of individuals in community governance. This metric counts the proportion of managers from individuals to all community managers (the sum of organizational managers and individual managers) during the statistical period. An appropriate individual manager ratio can ensure the community's independence and neutrality, avoiding excessive organizational control. This metric can reflect the community's governance openness and individual participation level.

# Assessment Model Algorithm

## Weight

The weights of each metric are equally distributed.

### Organizational Open Governance

3 metrics are equally distributed, with each metric having a weight of approximately 33.33%.

### Individual Open Governance

2 metrics are equally distributed, with each metric having a weight of 50%.

## Threshold

The thresholds we selected are based on big data observations of different types of open source projects.
