# Development and Build

Definition: Evaluating the security and trustworthiness of the development process, reflecting the project's development maturity and build quality.

# Assessment Model

**Code Review Quality**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| Dependency Reachable | [/api/v3/code_review_quality/dependency_reachable](https://oss-compass.org/dataHub#api_v3_code_review_quality_dependency_reachable) | 10 | 0.25 |
| Snippet Reference | [/api/v3/code_review_quality/compliance_snippet_reference](https://oss-compass.org/dataHub#api_v3_code_review_quality_compliance_snippet_reference) | 10 | 0.25 |
| Patent Risk | [/api/v3/code_review_quality/patent_risk_oin](https://oss-compass.org/dataHub#api_v3_code_review_quality_patent_risk_oin) | 10 | 0.25 |
| Test Coverage | [/api/v3/code_review_quality/ecology_test_coverage](https://oss-compass.org/dataHub#api_v3_code_review_quality_ecology_test_coverage) | 10 | 0.25 |

**Development Document Quality**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| README | [/api/v3/development_document_quality/ecology_readme](https://oss-compass.org/dataHub#api_v3_development_document_quality_ecology_readme) | 10 | 0.25 |
| Build Documentation | [/api/v3/development_document_quality/ecology_build_doc](https://oss-compass.org/dataHub#api_v3_development_document_quality_ecology_build_doc) | 10 | 0.25 |
| Interface Documentation | [/api/v3/development_document_quality/ecology_interface_doc](https://oss-compass.org/dataHub#api_v3_development_document_quality_ecology_interface_doc) | 10 | 0.25 |
| Committers File | [/api/v3/development_document_quality/ecology_maintainer_doc](https://oss-compass.org/dataHub#api_v3_development_document_quality_ecology_maintainer_doc) | 10 | 0.25 |

**Trusted Build**

| Metric | URL | Threshold | Weight |
| ------ | --- | --------- | ------ |
| Buildable | [/api/v3/trusted_build/trusted_build_success](https://oss-compass.org/dataHub#api_v3_trusted_build_trusted_build_success) | 100 | 0.25 |
| CI Integration | [/api/v3/trusted_build/ci_integration](https://oss-compass.org/dataHub#api_v3_trusted_build_ci_integration) | 1 | 0.25 |
| Build Metadata Available | [/api/v3/trusted_build/build_metadata_available](https://oss-compass.org/dataHub#api_v3_trusted_build_build_metadata_available) | 1 | 0.25 |
| Reproducible Build | [/api/v3/trusted_build/reproducible_build](https://oss-compass.org/dataHub#api_v3_trusted_build_reproducible_build) | 1 | 0.25 |

# Metrics in Assessment Model

## Code Review Quality

The code review quality model focuses on security and compliance during the code review process, ensuring code quality and intellectual property security.

### Dependency Reachable

- Definition: Whether the project's dependencies can be obtained normally.
- Weight: 25%
- Threshold: 10 (Reachable)

Dependency reachability is the foundation for ensuring project buildability. This metric uses a dependency reachability checker to detect whether all of the project's dependencies are accessible, outputting the proportion of reachable dependencies and a list of unreachable dependencies. If dependencies cannot be obtained, the project cannot be built and used normally. This metric reflects the project's dependency management level and sustainability.

### Snippet Reference

- Definition: Whether the project correctly references third-party code snippets.
- Weight: 25%
- Threshold: 10 (Compliant)

Snippet reference compliance is an important aspect of intellectual property protection. This metric uses the OAT scanner to detect the compliance of third-party snippet references within the project's code. Correctly referencing third-party code snippets can avoid intellectual property disputes and protect the rights of the project and users. This metric reflects the project's intellectual property management level.

### Patent Risk

- Definition: Whether the project has patent risks (based on the OIN patent pool).
- Weight: 25%
- Threshold: 10 (No Risk)

Patent risk is an important legal risk faced by open source projects. This metric checks the project's dependencies for patent risk based on the OIN patent pool, identifying whether potential patent infringement risks exist. Checking through the OIN patent pool can help projects avoid legal disputes. This metric reflects the project's legal risk management level.

### Test Coverage

- Definition: The test coverage rate of the project.
- Weight: 25%
- Threshold: 10 (Meets Standard)

Test coverage is an important indicator of code quality. High test coverage can ensure code stability and reliability, reducing defects and security risks. This metric reflects the project's quality assurance level.

## Development Document Quality

The development document quality model focuses on the completeness and standardization of project documentation, ensuring that the project is easy to understand and use.

### README

- Definition: Whether the project includes a README document.
- Weight: 25%
- Threshold: 10 (Included)

README is the project's facade and the first entry point for users to understand the project. This metric uses a README checker to detect whether a README file exists in the project's root directory and evaluates its content completeness. A complete README can help users quickly understand the project's functionality, installation, and usage methods. This metric reflects the project's documentation completeness.

### Build Documentation

- Definition: Whether the project includes build documentation.
- Weight: 25%
- Threshold: 10 (Included)

Build documentation is an important document guiding users to build the project. This metric uses a build documentation checker to detect whether the project contains build instructions. Complete build documentation can help users successfully build the project and lower the barrier to use. This metric reflects the project's user friendliness.

### Interface Documentation

- Definition: Whether the project includes interface documentation.
- Weight: 25%
- Threshold: 10 (Included)

Interface documentation is an important document guiding users to use the project API. This metric uses an interface documentation checker to detect whether the project contains API interface documentation. Complete interface documentation can help users correctly use project functions and improve development efficiency. This metric reflects the project's developer friendliness.

### Committers File

- Definition: Whether the project includes a Committers or Maintainers file.
- Weight: 25%
- Threshold: 10 (Included)

The Committers file records the project's core contributors and maintainers. This metric uses a maintainer documentation checker to detect whether the project contains a Committers or Maintainers file. A complete Committers file can help users understand the project's governance structure and contributors. This metric reflects the project's governance transparency.

## Trusted Build

The trusted build model focuses on the security and reproducibility of the build process, ensuring the trustworthiness of build results.

### Buildable

- Definition: Whether the project can be successfully built.
- Weight: 25%
- Threshold: 100 (Buildable)

Buildability is the foundation of project usability. This metric uses a build checker to execute the project build and count the build success rate. If the project cannot be built, it cannot be used by users. This metric reflects the project's build quality and usability.

### CI Integration

- Definition: Whether the project integrates a continuous integration (CI) system.
- Weight: 25%
- Threshold: 1 (Integrated)

CI integration is a standard practice in modern software development. This metric uses a CI checker to detect whether the project has configured CI workflows or CI configuration files. Through a CI system, the build and testing process can be automated to ensure code quality. This metric reflects the project's development process maturity.

### Build Metadata Available

- Definition: Whether the project's build metadata can be obtained.
- Weight: 25%
- Threshold: 1 (Available)

Build metadata includes build time, build environment, dependency versions, and other information. This metric uses a build metadata checker to detect whether the project outputs and provides obtainable build metadata. Obtainable build metadata can help users understand the build process and improve build traceability. This metric reflects the project's build transparency.

### Reproducible Build

- Definition: Whether the project supports reproducible builds.
- Weight: 25%
- Threshold: 1 (Supported)

Reproducible build means that the same source code can produce the same build results in different environments. This metric uses a reproducible build checker to compare whether the checksums of multiple build artifacts are consistent. Supporting reproducible builds can ensure the trustworthiness of build results and prevent the build process from being tampered with. This metric reflects the project's security maturity.

# Assessment Model Algorithm

## Weight

The weights of each metric are equally distributed.

### Code Review Quality

4 metrics are equally distributed, with each metric having a weight of 25%.

### Development Document Quality

4 metrics are equally distributed, with each metric having a weight of 25%.

### Trusted Build

4 metrics are equally distributed, with each metric having a weight of 25%.

## Threshold

The thresholds for the supply chain security assessment are determined based on the scoring rules of the openchecker inspection tool: compliance, documentation, and review metrics use a 0–10 scoring scale, with a full-score threshold of 10; binary metrics have a threshold of 1.
