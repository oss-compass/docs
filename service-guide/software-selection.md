# Open Source Software Selection Evaluation Service

The "Open Source Selection Evaluation Service" launched by OSS-Compass community builds a data-driven, quantifiable, and comparable selection support system, transforming "selection" from subjective experience-driven to indicator and data-driven intelligent decision-making process.

## Features

We have designed three core functions around the three most common problems in open source software selection:

1. **Evaluate Known Open Source Software**
   Want to know if a specific project is worth using? Enter the GitHub/Gitee address, and the system automatically generates a report covering four dimensions: legal compliance, technical ecosystem, lifecycle, and cybersecurity.

2. **Function Description-based Software Recommendation**
   Users only need to describe "what they want to do" by entering natural language function descriptions (e.g., "JS library for processing Excel"). The system uses large language models (such as DeepSeek) to generate summaries of project text information, uses translation models and word frequency enhancement to build multilingual, high-coverage keyword vectors. During query, the LLM understands user intent and extracts core semantics; finally, through vector semantic similarity and BM25 keyword matching comprehensive scoring, it completes recommendation ranking and outputs Top-N most relevant open source project recommendations.

3. **Find Similar Function Alternative Software**
   When users want to find similar alternatives to their current tools, they only need to enter the address of the currently used third-party library, and the system uses LLM to construct query items based on its description and keywords, outputting Top-N functionally similar alternative projects.

Various roles in the development process can solve problems through this function:

![](media/image6.png)

## Operation Guide

**Step1:** First visit our website: [https://oss-compass.org](https://oss-compass.org), click "All Services" in the navigation bar, click "Open Source Selection Evaluation" in the popup to enter the service homepage.

![](media/image7.png)

![](media/image8.png)

**Step2: Evaluate Known Open Source Software**

Enter the project address in the input box, click Find Project, search results will appear below, check and generate a report, click "My Reports" to enter the report list, click the report icon to view report details.

![](media/image9.png)

![](media/image10.png)

![](media/image11.png)

**Step3: Software Recommendation through Function Description**

Enter requirements in the input box, such as "JS library for processing word", select recommendation sources (multiple selections allowed), click Get Recommendations, and results will appear below.

![](media/image12.png)

**Step4: Find Similar Function Software**

Enter the known software name in the input box, select the input library source, then select the recommendation library source to get recommendations.

![](media/image13.png)
