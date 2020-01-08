ARG BASE_CONTAINER=jupyter/datascience-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Vaelek"

USER root

ENV JUPYTER_ENABLE_LAB="yes"
ENV ACCEPT_EULA="y"

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    unixodbc-dev \
    gnupg \
    curl \
&& curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
&& curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list \
&& apt-get update \
&& apt-get install -y --no-install-recommends msodbcsql17 \
&& rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN pip install ipython_sql pyodbc tensorflow keras psycopg2-binary
