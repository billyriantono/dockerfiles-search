FROM mcr.microsoft.com/dotnet/core/sdk:3.1

LABEL maintainer="Jerry Chang <jchang@assetic.com>"

ENV PATH="/root/.dotnet/tools:${PATH}"

RUN apt-get update && \
    apt-get -y --no-install-recommends install default-jre && \
    rm -rf /var/lib/apt/lists/* && \
    dotnet tool install --global dotnet-sonarscanner

WORKDIR /root