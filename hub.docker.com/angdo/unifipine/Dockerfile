FROM python:3.6.5-alpine3.6

ARG AzureDataBricksPAT

# Setting ENV variables, means we do not need to call 'databricks configure'
# Env variables can then be passed in manually e.g. `docker run -it -e "DATABRICKS_TOKEN=<value_of_token>" databricks-cli-alpine`
# or passed through from host env variables    e.g. `docker run -it -e DATABRICKS_TOKEN -e DATABRICKS_HOST databricks-cli-alpine`
ENV DATABRICKS_HOST "https://westeurope.azuredatabricks.net"
ENV DATABRICKS_TOKEN $AzureDataBricksPAT

RUN apk update && apk add bash

RUN pip install --upgrade pip
RUN pip install --upgrade databricks-cli


CMD ["/bin/bash"]
