---
title: Scorecard
slug: /metrics-models/software_artifact/robustness/scorecard
tags:
  - Metrics Models
  - Software Artifact
  - Robustness
  - Scorecard
description: Security metrics for open source projects based on OpenSSF Scorecard.
---

# Scorecard

Definition: Security metrics for open source projects based on OpenSSF Scorecard, used to evaluate the security and best practice adherence of a project.

# Metrics in the Metrics Model

Scorecard is an automated security tool used to assess the security risks of open source projects. This evaluation model is implemented with reference to the [Scorecard Checks documentation](https://github.com/ossf/scorecard/blob/main/docs/checks.md), evaluating the project's security status through checks in multiple dimensions.

## Binary Artifacts

- Definition: Checks if the project contains generated binary files.
- Score Range: 0-10
- Weight: 10%
- Risk Level: High
- Scoring Rule: 10 points if there are no unverified binary files in the repository, 1 point deducted for each unverified binary file, with a minimum of 0 points.

Including generated binary files increases user risk. Many programming language systems can generate executable files from source code (e.g., machine code from C/C++, `.class` files from Java, `.pyc` files from Python, etc.). If the source code repository contains executable files, users often use them directly, leading to many dangerous behaviors.

## Branch Protection

- Definition: Checks if the default and release branches are protected.
- Score Range: 0-10
- Weight: 10%
- Risk Level: High
- Scoring Rule: 10 points if both default and release branches are protected, 5 points if one is not, 0 points if neither is protected.

Branch protection allows maintainers to define rules to enforce certain workflows, such as requiring reviews or passing certain status checks before merging into the main branch, or preventing the rewriting of public history.

## CI Tests

- Definition: Checks if the project runs tests before merging PRs.
- Score Range: 0-10
- Weight: 8%
- Risk Level: Low
- Scoring Rule: (Number of merged PRs that passed CI tests / Total number of merged PRs) * 10
- Note: Not yet supported.

Running tests helps developers find errors early, which can reduce the number of vulnerabilities introduced into the project.

## CII Best Practices

- Definition: Checks if the project has an OpenSSF Best Practices badge.
- Score Range: 0-10
- Weight: 8%
- Risk Level: Low
- Scoring Rule: Gold 10 points, Silver 7 points, Passing 5 points, InProgress 2 points, No badge 0 points.

The OpenSSF Best Practices badge indicates whether a project follows a set of security-focused best practices for open source software development.

## Code Review

- Definition: Checks if the project requires manual code review (checks the last 30 merged PRs).
- Score Range: 0-10
- Weight: 10%
- Risk Level: High
- Scoring Rule: (Number of manual reviews / Number of PRs) * 10, 0 points if there are no PRs.

Reviews can detect various unexpected issues, including vulnerabilities that can be fixed immediately before merging, which improves code quality. Reviews can also detect or prevent attackers from trying to insert malicious code.

## Contributors

- Definition: Checks if the project has contributors from multiple organizations.
- Score Range: 0-10
- Weight: 5%
- Risk Level: Low
- Scoring Rule: 0 organizations 0 points, 1 organization 3.33 points, 2 organizations 6.67 points, 3 or more organizations 10 points.

This check attempts to determine if the project has recently had contributors from multiple organizations (e.g., companies).

## Dangerous Workflows

- Definition: Checks if the workflow has dangerous code patterns.
- Score Range: 0-10
- Weight: 10%
- Risk Level: Critical
- Scoring Rule: Not scored if no workflow is found, 10 points if no dangerous patterns are found in the workflow, 0 points if any dangerous pattern is found.

This check determines if the project's workflow contains dangerous code patterns. These patterns include untrusted code checkouts, logging contexts and secrets, or using potentially untrusted input in scripts.

## Dependency Update Tool

- Definition: Checks if the project uses a dependency update tool.
- Score Range: 0-10
- Weight: 8%
- Risk Level: High
- Scoring Rule: 10 points if any dependency update tool is detected or if commits from a dependency update bot are found in the Git history, otherwise 0 points.
- Note: Not yet supported.

Outdated dependencies make a project vulnerable to known defects. These tools automate the process of updating dependencies by scanning for outdated or insecure requirements.

## Fuzzing

- Definition: Checks if the project uses fuzzing.
- Score Range: 0-10
- Weight: 5%
- Risk Level: Medium (vulnerabilities may exist in the code)
- Scoring Rule: 10 points if any fuzzing tool is detected, otherwise 0 points.

Fuzzing is the practice of inputting unexpected or random data into a program to expose errors. Regular fuzzing is important for detecting vulnerabilities that could be exploited by others.

## License

- Definition: Checks if the project has a license.
- Score Range: 0-10
- Weight: 5%
- Risk Level: Low
- Scoring Rule: No license 0 points, non-approved license (not FSF/OSI) 9 points, approved license (FSF/OSI) 10 points. See [approved licenses (FSF/OSI)](https://spdx.org/licenses/).

A license provides users with information on how the source code can be used. The lack of a license hinders any type of security review or audit and creates legal risks for potential users.

## Maintained

- Definition: Checks if the project is actively maintained.
- Score Range: 0-10
- Weight: 8%
- Risk Level: High
- Scoring Rule: (Number of commits in the last 90 days + Number of issues created in the last 90 days) / 13 * 10

An inactive project may not be patched, its dependencies may not be patched, and it may not be actively tested and used.

## Packaging

- Definition: Checks if the project is released as a package.
- Score Range: 0-10
- Weight: 5%
- Risk Level: Medium
- Scoring Rule: Not scored if no automated packaging workflow is detected, 10 points if a packaging workflow is detected.

Packages provide users with a simple way to download, install, update, and uninstall software through a package manager. In particular, they enable users to easily receive security patches as updates.

## Pinned Dependencies

- Definition: Checks if the project pins its dependencies.
- Score Range: 0-10
- Weight: 8%
- Risk Level: Medium
- Scoring Rule: Total score = Σ(number of pinned dependencies × weight) / Σ(total number of dependencies × weight)
  - Official platform Actions weight 2 (Actions with names starting with `actions/` or `gitcode/` are considered official GitCode Actions)
  - Third-party Actions weight 8 (GitCode Actions not starting with `actions/` or `gitcode/` are considered third-party Actions)
  - Other dependency types weight 10 (Container images in Dockerfiles, dependencies executed after download, Go command dependencies, Chocolatey package manager dependencies, NPM package dependencies, Python pip package dependencies, NuGet package dependencies, etc.)

"Pinned dependencies" are dependencies explicitly set to a specific hash rather than allowing a mutable version or version range. Pinning dependencies reduces security risks.

## SAST

- Definition: Checks if the project uses Static Application Security Testing.
- Score Range: 0-10
- Weight: 5%
- Risk Level: Medium
- Scoring Rule: 10 points if other SAST tools (Sonar, Snyk, Pysa, Qodana, etc.) or CodeQL configuration are detected, otherwise 0 points.

SAST is testing of source code before the application is run. Using SAST tools can prevent known classes of errors from being unintentionally introduced into the codebase.

## SBOM

- Definition: Checks if the project maintains a Software Bill of Materials.
- Score Range: 0-10
- Weight: 5%
- Risk Level: Medium
- Scoring Rule: 10 points if an SBOM file is found in the release package, 0 points if no SBOM file is detected.

An SBOM can provide users with information about a project's dependencies, enabling them to identify vulnerabilities in the software supply chain.

## Security Policy

- Definition: Checks if the project has a published security policy.
- Score Range: 0-10
- Weight: 5%
- Risk Level: Medium
- Scoring Rule: 0 points if `SECURITY.md` file does not exist, +6 points if `SECURITY.md` has a URL link or email address, +3 points if `SECURITY.md` contains actual text content, +1 point if it contains vulnerability disclosure information.

A security policy (usually a `SECURITY.md` file) provides users with information about what constitutes a vulnerability and how to report it securely.

## Signed Releases

- Definition: Checks if the project cryptographically signs its release artifacts.
- Score Range: 0-10
- Weight: 8%
- Risk Level: High
- Scoring Rule: Not scored if there are no releases, (Number of signed releases in the last 5 releases / 5) * 10.

Signed releases prove the origin of the artifacts. This check looks for signature files in the project's last five release assets.

## Token Permissions

- Definition: Checks if automated workflow tokens follow the principle of least privilege.
- Score Range: 0-10
- Weight: 8%
- Risk Level: High
- Scoring Rule: Not scored if there is no workflow, 10 points if all workflows follow the principle of least privilege, 0 points if a serious over-permission issue like `write-all` is detected.

This check determines if the project's automated workflow tokens follow the principle of least privilege. This is important because an attacker could use a compromised token with write permissions to push malicious code into the project.

## Vulnerabilities

- Definition: Checks if the project has unfixed vulnerabilities.
- Score Range: 0-10
- Weight: 8%
- Risk Level: High
- Scoring Rule: 10 - number of vulnerabilities found.

This check determines if the project has open, unfixed vulnerabilities in its own codebase or its dependencies. Open vulnerabilities are easy for attackers to exploit and should be fixed as soon as possible.

## Webhooks

- Definition: Checks if WebHooks are configured with token authentication.
- Score Range: 0-10
- Weight: 5%
- Risk Level: Critical
- Scoring Rule: 10 points if there are no WebHooks, (Number of WebHooks configured with a secret / Total number of WebHooks) × 10.

This check determines if the WebHooks defined in the repository are configured with a token to verify the origin of the request.

# Metrics Model Algorithm

## Weight Allocation

Weights are assigned based on the risk level and importance of each check:

- Critical Risk: 10% weight
- High Risk: 8-10% weight
- Medium Risk: 5-8% weight
- Low Risk: 5% weight

## Metric Score

The maximum score for a metric is 10, and the minimum is 0.

## Scoring Mechanism

Each check is scored from 0-10 based on its implementation level, and the final score is calculated as a weighted sum. The total score reflects the overall security posture of the project.
The corresponding formula is: Project Score = Σ(Metric Score × Metric Weight) / Σ(Metric Weight).

# References

- [Scorecard Checks Documentation](https://github.com/ossf/scorecard/blob/main/docs/checks.md)

# Contributors

## Backend

- Yehui Wang
- Shengbao Li

## Metrics Model

- Yehui Wang
- Guoqiang Qi
- Shengbao Li