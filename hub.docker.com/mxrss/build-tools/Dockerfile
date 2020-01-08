FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
LABEL image.maintainer="mike.roth@mxrss.com"
LABEL image.created="2019-06-29"
LABEL image.description="This image has the vsts tooling in addition to dotnet core and powershell with psake installed. This is used as a base for my vsts agent images"
LABEL image.runasroot=True
LABEL image.warning="Runs as root, needs some refinement i dont have time for right now to run as another user"
LABEL image.name="build-tools"

ENV AGENT_ALLOW_RUNASROOT True
ENV AZURE_CLI_VERSION "0.10.13"
ENV NODEJS_APT_ROOT "node_6.x"
ENV NODEJS_VERSION "6.10.0"
ENV TFS_URL = ""
ENV TFS_AUTH_USERNAME = ""
ENV TFS_AUTH_PASSWORD = ""
ENV TFS_BUILD_POOL = ""

WORKDIR /app/Agent
RUN groupadd -g 999 builder && \
    useradd -r -u 999 -g builder builder && \
    mkdir -p /home/builder && \
    chown builder:builder /home/builder

ADD https://vstsagentpackage.azureedge.net/agent/2.150.0/vsts-agent-linux-x64-2.150.0.tar.gz /app
RUN tar -xvf /app/vsts-agent-linux-x64-2.150.0.tar.gz
RUN apt-get update && apt-get install curl gnupg apt-transport-https -y
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list'
RUN  apt-get update && apt-get install powershell  -y && \
     pwsh -c 'Install-Module -Name psake  -Force -Scope AllUsers'
RUN curl -sL https://aka.ms/InstallAzureCLIDeb |  bash
COPY ./exec.sh /app/Agent/exec.sh
RUN chmod +x /app/Agent/exec.sh
CMD ["/app/Agent/exec.sh"]
ENTRYPOINT /bin/bash