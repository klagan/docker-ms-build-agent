# Getting started

[source](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#linux)

## Build docker image

```
docker build -t azdo-agent:latest .
```

## Start agent

```
docker run -d --restart always -e AZP_URL=https://dev.azure.com/<ORGANISATION>-e AZP_TOKEN=<PAT> -e AZP_AGENT_NAME=<AGENT-NAME> AZP_POOL=<POOL> azdo-agent:latest
```
