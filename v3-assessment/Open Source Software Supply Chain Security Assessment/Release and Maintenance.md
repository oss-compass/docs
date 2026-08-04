# Release and Maintenance

Definition: Evaluating the security of the release process and maintenance management level, reflecting the project's release quality and continuous maintenance capability.

# Assessment Model

**Release Quality**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| SBOM Check | [/api/v3/release_quality/sbom_in_release](https://oss-compass.org/dataHub#api_v3_release_quality_sbom_in_release) | 10 | 0.25 |
| Binary Artifact Included | [/api/v3/release_quality/security_binary_artifact](https://oss-compass.org/dataHub#api_v3_release_quality_security_binary_artifact) | 1 | 0.25 |
| Package Signature | [/api/v3/release_quality/security_package_sign](https://oss-compass.org/dataHub#api_v3_release_quality_security_package_sign) | 10 | 0.25 |
| Release Notes | [/api/v3/release_quality/lifecycle_release_note](https://oss-compass.org/dataHub#api_v3_release_quality_lifecycle_release_note) | 10 | 0.25 |

**Maintenance Management**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| Lifecycle Statement | [/api/v3/maintenance_management/lifecycle_statement](https://oss-compass.org/dataHub#api_v3_maintenance_management_lifecycle_statement) | 10 | 0.50 |
| Average Vulnerability Fix Time | [/api/v3/maintenance_management/avg_vulnerability_fix_time](https://oss-compass.org/dataHub#api_v3_maintenance_management_avg_vulnerability_fix_time) | 90 days | 0.50 |

# Metrics in Assessment Model

## Release Quality

The release quality model focuses on the security and standardization of the release process, ensuring the integrity and trustworthiness of release versions.

### SBOM Check

- Definition: Whether the release version includes a Software Bill of Materials (SBOM).
- Weight: 25%
- Threshold: 10 (Included)

SBOM (Software Bill of Materials) is a software bill of materials that records all components and dependencies contained in the software. This metric uses a release checker to detect whether the project's release version is accompanied by an SBOM. Including SBOM can help users understand the composition of the software and identify potential security risks. This metric reflects the project's supply chain transparency.

### Binary Artifact Included

- Definition: Whether the release version includes binary artifacts that should not exist.
- Weight: 25%
- Threshold: 1 (Compliant)

Binary artifact review is an important part of release security. This metric uses a binary checker and the OAT scanner to detect whether binary files that should not have been committed exist in the project's release version, scoring on a 0–10 scale; the fewer binary artifacts, the higher the score. Avoiding mixing binary artifacts into source code releases can reduce supply chain security risks. This metric reflects the project's release security management level.

### Package Signature

- Definition: Whether the release version has been digitally signed.
- Weight: 25%
- Threshold: 10 (Signed)

Package signature is an important measure to ensure software integrity and authenticity. This metric uses a release checker to detect whether the project's release version has digitally signed the release artifacts. Through digital signatures, the source and integrity of software packages can be verified, preventing software packages from being tampered with. This metric reflects the project's security maturity.

### Release Notes

- Definition: Whether the release version includes release notes.
- Weight: 25%
- Threshold: 10 (Included)

Release Notes record version changes, new features, fixed issues, and other information. This metric uses a release checker to detect whether the project's release version is accompanied by Release Notes. Complete Release Notes can help users understand version changes and make upgrade decisions. This metric reflects the project's documentation completeness.

## Maintenance Management

The maintenance management model focuses on the project's maintenance status and response capability, ensuring that the project receives continuous maintenance.

### Lifecycle Statement

- Definition: Whether the project declares its lifecycle status.
- Weight: 100%
- Threshold: 10 (Declared)

Lifecycle statement informs users of the project's current status (such as active, maintenance, archived, etc.). This metric uses a lifecycle documentation checker to detect whether the project declares its lifecycle status. A clear lifecycle statement can help users understand the project's maintenance status and make usage decisions. This metric reflects the project's transparency and user care.

### Average Vulnerability Fix Time

- Definition: The average time for the project to fix security vulnerabilities (to be implemented).
- Weight: 0%
- Threshold: 30 days

Average vulnerability fix time is an important indicator of the project's security response capability. This metric uses a vulnerability scanner to collect the duration from public disclosure to fix for disclosed security vulnerabilities and calculates the average (if the vulnerability policy checker has data, it serves as a supplementary source). A shorter fix time can reduce the time users are exposed to security risks, protecting user security. This metric reflects the project's security maintenance capability.

# Assessment Model Algorithm

## Weight

The weights of each metric are equally distributed.

### Release Quality

4 metrics are equally distributed, with each metric having a weight of 25%.

### Maintenance Management

The weight of Lifecycle Statement is 100%.

## Threshold

The thresholds for the supply chain security assessment are determined based on the scoring rules of the openchecker inspection tool: compliance, documentation, and review metrics use a 0–10 scoring scale, with a full-score threshold of 10; binary metrics have a threshold of 1.
