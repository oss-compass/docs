---
id: software-artifact-robustness-overview
title: Software Artifact-Robustness
slug: /dimensions-define/software_artifact/robustness
sidebar_label: Overview
tags:
 - Metrics Models
 - Software Artifact
 - Robustness
description: The ability of an ecosystem to recover from internal or external conflicts.
---

# Robustness

Definition: The ability of an ecosystem to recover from internal or external conflicts.

# Metrics Models

## [Scorecard](./scorecard.md)

| Metric Name | Definition | Score Range | Weight | Risk Level |
|---|---|---|---|---|
| [Binary Artifacts](./scorecard.md#binary-artifacts) | Checks whether the project contains generated binary files | 0-10 | 10% | High |
| [Branch Protection](./scorecard.md#branch-protection) | Checks if the default and release branches are protected | 0-10 | 10% | High |
| [CI Tests](./scorecard.md#ci-tests) | Checks if the project runs tests before merging PRs | 0-10 | 8% | Low |
| [CII Best Practices](./scorecard.md#cii-best-practices) | Checks if the project has an OpenSSF Best Practices badge | 0-10 | 8% | Low |
| [Code Review](./scorecard.md#code-review) | Checks if the project requires manual code review | 0-10 | 10% | High |
| [Contributors](./scorecard.md#contributors) | Checks if the project has contributors from multiple organizations | 0-10 | 5% | Low |
| [Dangerous Workflow](./scorecard.md#dangerous-workflow) | Checks for dangerous code patterns in GitHub Actions workflows | 0-10 | 10% | Critical |
| [Dependency Update Tool](./scorecard.md#dependency-update-tool) | Checks if the project uses a dependency update tool | 0-10 | 8% | High |
| [Fuzzing](./scorecard.md#fuzzing) | Checks if the project uses fuzz testing | 0-10 | 5% | Medium |
| [License](./scorecard.md#license) | Checks if the project has a license | 0-10 | 5% | Low |
| [Maintained](./scorecard.md#maintained) | Checks if the project is actively maintained | 0-10 | 8% | High |
| [Packaging](./scorecard.md#packaging) | Checks if the project is published as a package | 0-10 | 5% | Medium |
| [Pinned Dependencies](./scorecard.md#pinned-dependencies) | Checks if the project pins its dependencies | 0-10 | 8% | Medium |
| [SAST](./scorecard.md#sast) | Checks if the project uses static application security testing | 0-10 | 5% | Medium |
| [SBOM](./scorecard.md#sbom) | Checks if the project maintains a Software Bill of Materials | 0-10 | 5% | Medium |
| [Security Policy](./scorecard.md#security-policy) | Checks if the project has a security policy | 0-10 | 5% | Medium |
| [Signed Releases](./scorecard.md#signed-releases) | Checks if the project cryptographically signs its release artifacts | 0-10 | 8% | High |
| [Token Permissions](./scorecard.md#token-permissions) | Checks if the automated workflow tokens follow the principle of least privilege | 0-10 | 8% | High |
| [Vulnerabilities](./scorecard.md#vulnerabilities) | Checks if the project has unfixed vulnerabilities | 0-10 | 8% | High |
| [Webhooks](./scorecard.md#webhooks) | Checks if webhooks are configured with token authentication | 0-10 | 5% | Critical |

## [Criticality Score](./criticality_score.md)

| Metric Name | Definition | Threshold | Weight |
|---|---|---|---|
| [Created Since](./criticality_score.md#created-since) | Time since project creation (in months) | 9.523% | 120 |
| [Updated Since](./criticality_score.md#updated-since) | Time since last project update (in months) | -9.523% | 120 |
| [Contributor Count](./criticality_score.md#contributor-count) | Number of project contributors (with commit history) | 19.047% | 5000 |
| [Org Count](./criticality_score.md#org-count) | Number of different organizations contributors belong to | 9.523% | 10 |
| [Commit Frequency](./criticality_score.md#commit-frequency) | Average weekly commits in the last year | 9.523% | 1000 |
| [Recent Releases Count](./criticality_score.md#recent-releases-count) | Number of releases in the last year | 4.761% | 26 |
| [Closed Issues Count](./criticality_score.md#closed-issues-count) | Number of closed issues in the last 90 days | 4.761% | 5000 |
| [Updated Issues Count](./criticality_score.md#updated-issues-count) | Number of updated issues in the last 90 days | 4.761% | 5000 |
| [Comment Frequency](./criticality_score.md#comment-frequency) | Average comments per issue in the last 90 days | 9.523% | 15 |
| [Dependents Count](./criticality_score.md#dependents-count) | Number of times the project is mentioned by other projects in commit messages | 19.047% | 50 |

## [CII Best Practices Badge](./cii_best_badge.md)

| Metric Name | Definition |
|---|---|
| [Badge Level](./cii_best_badge.md) | Assesses whether an open source project adopts a set of security-focused best development practices |