# Getting started

[source](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#linux)

## Build docker image

```
docker build -t azdo-agent:latest .
```

## Start agent

```
docker run -d --restart always --name <CONTAINER NAME> -e AZP_URL=https://dev.azure.com/<ORGANISATION>-e AZP_TOKEN=<PAT> -e AZP_AGENT_NAME=<AGENT-NAME> AZP_POOL=<POOL> azdo-agent:latest
```

## Connect to running container to view output

```
docker attach --sig-proxy=false <CONTAINER NAME / CONTAINER ID>
```

## Run command in container

```
docker exec -it <CONTAINER NAME/CONTAINER ID> <COMMAND>
```

## Stop all containers

```
docker stop $(docker ps -a -q)
```

## Remove all containers
```
docker rm $(docker ps -a -q)
```

## ENV vs ARG

`ARG` is for build time input
`ENV` is for run time input

If, we need the **container** to accept different vales for environment variables then we would use `ENV`
If, we need to set specific values for the **image** then we would use `ARG`

`ARG` is baked into the image for every instance to use as a constant
`ENV` is variable per container

We can get the best of both worlds if we do something like this:

```
ARG myVar=someValue
ENV myVar=$(myVar)
```

This allows us to set default constants on the `ARG`, but also override them by invoking `ENV`
