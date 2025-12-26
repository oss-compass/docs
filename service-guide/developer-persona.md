# Developer Persona Evaluation Service

In the thriving open source ecosystem, developers as the core driving force, insights into their behavioral patterns, technical capabilities, and collaboration tendencies have become key to project sustainability. The "Developer Persona Evaluation Service" launched by OSS-Compass community, leveraging a data-driven multi-dimensional modeling system, provides precise developer capability assessment for open source project managers, enterprise technical teams, and researchers, helping to discover high-value contributors and optimize open source collaboration efficiency.

## Features

**1. Data Foundation**

The service relies on OSS-Compass open source data hub, integrating the following data sources:
- GHArchive dataset: Captures GitHub full historical events (Commit, PR, Issue, etc.). Project activity data: Obtains user behavior records for target projects and related projects through GitHub API.
- User attribute information: Including developers' programming language preferences, project experience, affiliated organizations, and other structured data.
- Uses "snowball method" to build contributor networks: Starting from initial "seed" projects, scanning active users' full project activity events, gradually expanding the related user pool, forming a behavior database covering tens of millions of developers.

**2. Build Dual-Dimension Persona System**

**Skill Persona: Technical Capability Quantitative Assessment**
- Technology stack match: Analyze developers' programming language usage proportion, API/library experience, and project participation history to calculate technical fit with target projects.
- Activity and influence: Count Commit, PR, Issue, and other event quantities, combined with global ranking, to evaluate their productivity in the open source community.
- Project role identification: Distinguish roles such as "organization manager", "visitor contributor", "individual developer", etc.

**Willingness Persona: Deep Analysis of Collaboration Tendencies**
- Sentiment analysis: Use natural language processing technology to parse sentiment polarity (positive/neutral/negative) in developers' Issue/PR comments.
- Social network modeling: Build developer collaboration network graphs, evaluating their hub role in the community through degree centrality, betweenness centrality, and other metrics.
- Cross-project investment distribution: Compare developers' activity proportion in target projects versus other projects to predict their likelihood of joining new communities.

Various roles in the development process can solve problems through this function:

![](media/image14.png)

## Operation Guide

**Step1:** First, visit the OSS-Compass website: [https://oss-compass.org](https://oss-compass.org), enter the developer's GitHub account address (e.g., Hixie) in the homepage input box, click "Developer Name" to get the persona report.

![](media/image15.png)

**Step2:** The developer persona service generates a report containing the following modules:

- **Basic Information:** Developer basic info, affiliated organization, country; activity ranking (e.g., Commits global top 20%, Issues global top 5%), technology stack distribution.
- **Project Contribution Details:** Roles in each repository (organization manager/organization participant/individual affiliate/individual participant), contribution type proportion.
- **Contributor Collaboration Network:** Collaboration relationship graph between the current developer and other developers.
- **Time Series Analysis:** Monthly Code Commit frequency, Issue update count, and other trend charts for the past year.

![](media/image16.png)

![](media/image17.png)

![](media/image18.png)

![](media/image19.png)

![](media/image20.png)
