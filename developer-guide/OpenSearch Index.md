# OpenSearch Index

```json
{
    "repo_index": "github-repo_enriched",
    "git_index": "github-git_enriched",
    "issue_index": "github-issues_enriched",
    "pr_index": "github-pulls_enriched",
    "contributors_index": "github-contributors_org_repo",
    "contributors_enriched_index": "github-contributors_org_repo_enriched",    
    "out_index": "compass_metric_model_custom_v1"
}
```

### **索引说明**

1. **`repo_index`（github-repo_enriched）**
   - 存储 GitHub **仓库（Repository）** 的数据，包括名称、fork数量、start数量信息。
2. **`git_index`（github-git_enriched）**
   - 存储 Git 相关数据，包括commit message、commit hash、仓库名称，标题、提交人、提交时间等信息。
3. **`issue_index`（github-issues_enriched）**
   - 存储 GitHub **Issue（问题）** 的数据，包括 Issue 标题、状态、创建者、标签、创建时间、关闭时间等信息。
4. **`pr_index`（github-pulls_enriched）**
   - 存储 GitHub **Pull Request（合并请求）** 的数据，包括 PR 标题、提交记录、审核状态、审查评论数量、标签、创建时间、更新时间、关闭时间、是否合并等。
5. **`contributors_index`（github-contributors_org_repo）**
   - 存储 GitHub 仓库的贡献者数据，包括贡献者的用户名、贡献时间、第一次贡献时间、最后一次贡献时间等信息。
6. **`contributors_enriched_index`（github-contributors_org_repo_enriched）**
   - **增强版贡献者索引**，包括贡献者的用户名、贡献类型、是否为机器人、仓库名称信息。
7. **`out_index`（compass_metric_model_custom_v1）**
   - **最终输出索引**，用于存储计算后的指标数据。