FROM mcr.microsoft.com/dotnet/core/sdk:2.2.207

LABEL maintainer="Mikhail Merkulov <mikhail.merkulov@itomy.ch>"
ENV COMPOSE_VERSION 1.24.0
ENV DOCKER_VERSION 5:18.09.1~3-0~debian-stretch
ENV HADOLINT_VERSION 1.17.3
ENV VAULT_VERSION 1.3.0
#install dependencies
RUN curl -L https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-Linux-x86_64 > /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
RUN apt-get update \
    && apt-get install \
    host \
    dnsutils \
    jq \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common \
    nginx \
    openjdk-8-jre \
    -y --no-install-recommends \
    && apt-get clean -y
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - 
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" 
RUN apt-get update && apt-get install \
    python-pip \
    docker-ce=$DOCKER_VERSION \
    docker-ce-cli=$DOCKER_VERSION \
    containerd.io \
    zip -y
RUN curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
RUN pip install \
    awscli \
    ansible \
    ansible-lint \
    --upgrade \
    && apt-get clean -y
RUN dotnet tool install --global Amazon.Lambda.Tools --version 3.3.1 && \
    dotnet tool install --global dotnet-sonarscanner --version 4.7.1
RUN wget https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_amd64.zip -O vault.zip \
    &&  unzip vault.zip -d /usr/bin/ && rm vault.zip
RUN curl -fsSL https://goss.rocks/install | sh
RUN curl -L https://github.com/hadolint/hadolint/releases/download/v${HADOLINT_VERSION}/hadolint-Linux-x86_64 > /usr/local/bin/hadolint
RUN chmod +x /usr/local/bin/hadolint
ENV PATH=$PATH:~/.local/bin:~/.dotnet/tools
