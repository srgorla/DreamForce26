# Exercise 1, Task 1: Agentforce Data Library configuration

The version-controlled request is
[`data-library.json`](../../../config/workshops/service-assistant-dynamic-plans/data-library.json).
This is an Agentforce Connect REST API request, not Metadata API XML, and cannot
be deployed with `sf project deploy start`.

On 2026-09-19, the target org's API 67.0 metadata describe exposed no Data Library
or AI Grounding Library metadata type. Salesforce documents library creation
through the [Agentforce Connect REST API](https://developer.salesforce.com/docs/platform/connect-rest-api/references/connect-rest-api-agentforce).

## Verified prerequisites

- The authenticated training org responds to the library list endpoint (HTTP 200).
- The library list was empty at the time of verification.
- `Knowledge__kav` has `Title` (string), `Summary` (textarea), and
  `Answer__c`, `Detail__c`, `Question__c` (textarea).
- The request uses the guide's identifying and content fields. It applies no
  public-only restriction or data category filter, consistent with the guide.
- The default data space is used by omitting `dataSpaceScopeId`.

## Create the library

Run commands from the project root. First check for an existing library with
developer name `Agentforce_Service_Assistant_Library`; do not create a duplicate.

```sh
sf api request rest /services/data/v67.0/einstein/data-libraries \
  --method GET \
  --target-org DF26_Service_Cloud_Assistant_Dynamic_Plans --json
```

The following command creates the library and starts provisioning:

```sh
sf api request rest /services/data/v67.0/einstein/data-libraries \
  --method POST \
  --header 'Content-Type: application/json' \
  --body @config/workshops/service-assistant-dynamic-plans/data-library.json \
  --target-org DF26_Service_Cloud_Assistant_Dynamic_Plans --json
```

Check the HTTP status in the CLI response as well as its exit status. Expected:
HTTP 201 and a `libraryId`. Use that returned ID to inspect the library and poll
its status, replacing `LIBRARY_ID` below:

```sh
sf api request rest /services/data/v67.0/einstein/data-libraries/LIBRARY_ID \
  --method GET \
  --target-org DF26_Service_Cloud_Assistant_Dynamic_Plans --json

sf api request rest /services/data/v67.0/einstein/data-libraries/LIBRARY_ID/status \
  --method GET \
  --target-org DF26_Service_Cloud_Assistant_Dynamic_Plans --json
```

Confirm the stored field selections match the request. The library must reach
`READY` before use by the agent. Knowledge provisioning starts automatically;
do not call the file-library indexing endpoint.

## Current status

Created in `DF26_Service_Cloud_Assistant_Dynamic_Plans` on 2026-09-19 using the
committed JSON request. The prior library list was empty. Creation returned
HTTP 201 and library ID `1JDgL000009JgcfWAC`; the response confirmed all configured
field selections. A subsequent status check returned HTTP 200 and `IN_PROGRESS`.
Provisioning readiness is pending. Do not repeat the creation request in this org.
