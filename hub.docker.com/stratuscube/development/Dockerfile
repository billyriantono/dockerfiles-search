FROM ubuntu:18.04

LABEL author="Mark Pro"
LABEL maintainter="StratusCube Core Dev Team"
LABEL company="StratusCube LLC"

ENV DOTNET_CLI_TELEMETRY_OPTOUT=1

RUN apt-get update \
    && apt-get install -y curl apt-transport-https gnupg2 \
    && curl https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb \
    -o packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb \
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && ACCEPT_EULA=Y \
    apt-get install -y openjdk-8-jdk-headless dotnet-sdk-2.2 mssql-tools unixodbc-dev yarn \
    nodejs powershell \
    && yarn global add newman \
    && echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile \
    && echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc source ~/.bashrc

EXPOSE 80
EXPOSE 443