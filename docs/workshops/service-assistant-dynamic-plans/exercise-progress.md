# Agentforce Service Assistant (Dynamic Plans)

[Student and exercise guides](README.md#guides)

Project target org: `DF26_Service_Cloud_Assistant_Dynamic_Plans`.

## Commit workflow

Complete tasks in guide order. After each task, retrieve its supported metadata,
review the changes, record validation here, and create a separate commit using
the task identifier below. For configuration or testing that cannot be retrieved
as metadata, commit a concise record of the settings and observed results.
Never commit passwords, tokens, authentication files, or customer interaction data.
Mark a task complete only after its result has been verified.

## Task checklist

| ID | Task | Status |
| --- | --- | --- |
| setup-01 | Obtain training org credentials | Already handled by user; existing CLI authentication used |
| setup-02 | Log in to training org | Verified: authenticated Organization query succeeded |
| ex1-task1 | Create Agentforce Service Assistant Library | Created and configuration verified; provisioning IN_PROGRESS |
| ex2-task1 | Enable Agentforce and Service Assistant | Complete: Agentforce metadata verified; Service Assistant confirmed by user |
| ex2-task2 | Create Service Assistant agent | Pending |
| ex2-task3 | Create Order Refund subagent; add General CRM and General FAQ | Pending |
| ex2-task4 | Connect data library, show sources, activate agent | Pending |
| ex2-task5 | Configure Service AI Grounding | Pending |
| ex2-task6 | Create and activate custom Email-origin eligibility flow; configure mappings | Pending |
| ex2-task7 | Enable Dynamic Plans, default agent, and Service Assistant for Cases | Pending |
| ex2-task8 | Assign Data Cloud User permission set to ServicePlanner User | Pending |
| ex2-task9 | Add Service Assistant to Case record page and verify org default | Pending |
| ex3-task1 | Validate Service Assistant on the guide's training case | Pending |

## Validation notes

### setup-02: verify existing login

On 2026-09-19, the following read-only query succeeded against the project target:

```sh
sf data query --target-org DF26_Service_Cloud_Assistant_Dynamic_Plans --query 'SELECT Id, Name, IsSandbox FROM Organization' --json
```

The query returned one Organization record named `EPIC OrgFarm` with
`IsSandbox = false`. No credentials or tokens were recorded.

### ex1-task1: create the data library

On 2026-09-19, checked the library list (HTTP 200, no existing libraries), then
executed the committed `data-library.json` creation request. Salesforce returned
HTTP 201 with library ID `1JDgL000009JgcfWAC` and status `IN_PROGRESS`.
The response confirmed `Title` and `Summary` as identifying fields and
`Answer__c`, `Detail__c`, `Question__c` as content fields, with no category or
public-only restriction. A subsequent status request returned HTTP 200 and
`IN_PROGRESS`. Creation is complete; `READY` must be verified before agent use.

### ex2-task1: enable Agentforce and Service Assistant

On 2026-09-19, the user confirmed completing both enablement steps in Salesforce
Go. Retrieved `Settings:AgentPlatform` successfully from the training org:

```sh
sf project retrieve start --metadata Settings:AgentPlatform \
  --target-org DF26_Service_Cloud_Assistant_Dynamic_Plans --json --wait 5
```

The retrieved [AgentPlatform settings](../../../force-app/main/default/settings/AgentPlatform.settings-meta.xml)
contain `enableAgentPlatform=true`. Service Assistant's initial enablement is
recorded based on the user's confirmation; it has not been independently
verified through metadata or API. A Data Library status check during this task
still returned `IN_PROGRESS`.

## First task: create the data library

For creation from source, use the [API configuration and commands](data-library.md).
The manual Setup steps below are an alternative.

In Setup, open **Agentforce Data Library**, choose **Add Data**, then
**Add Knowledge Articles**. Configure:

- Name: `Agentforce Service Assistant Library`
- API name: `Agentforce_Service_Assistant_Library`
- Description: The Agentforce Data Library stores resort knowledge articles for the Service Assistant to instantly retrieve during guest interactions.
- Identifying fields: **Title**, **Summary**
- Content fields: **Answer**, **Detail**, **Question**

Save. The library can build while subsequent tasks proceed; it must reach
**Ready** before Service Assistant can successfully use it.
