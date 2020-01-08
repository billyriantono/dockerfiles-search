FROM ubuntu:18.04

# Upstream maintainer Fabian Grutschus
LABEL maintainer="tonidy2@gmail.com"

ARG TOOL_VERSION=17.4.1.1-1
ENV MSSQLTOOLS_VERSION=$TOOL_VERSION
ENV PATH /opt/mssql-tools/bin:$PATH

RUN apt-get update \
    && apt-get install -y curl apt-transport-https locales gnupg \
    && locale-gen "en_US.UTF-8" \
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | tee /etc/apt/sources.list.d/msprod.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17 mssql-tools=$MSSQLTOOLS_VERSION unixodbc-dev \
    && apt-get remove -y curl apt-transport-https \
    && rm -f /etc/apt/sources.list.d/msprod.list \
    && rm -rf /var/lib/apt/lists/*

## should be set after locale was generate, overwise triggers warnings
ENV LANG="en_US.UTF-8" LANGUAGE="en_US.UTF-8" LC_ALL="en_US.UTF-8"

CMD ["sqlcmd"]
