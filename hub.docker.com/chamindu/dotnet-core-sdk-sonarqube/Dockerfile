FROM openjdk:8u181-jre-stretch

LABEL maintainer="Chamindu Munasinghe <cmunasinghe@gmail.com>"

RUN apt-get update \
    && apt-get install -y apt-transport-https \
    && curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /etc/apt/trusted.gpg.d/microsoft.asc.gpg \
    && curl https://packages.microsoft.com/config/debian/9/prod.list --output /etc/apt/sources.list.d/microsoft-prod.list \
    && curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get update \
    && apt-get install -y dotnet-sdk-2.2 nodejs
    
RUN dotnet tool install --global dotnet-sonarscanner --version 4.5.0

ENV PATH="${PATH}:/root/.dotnet/tools"


