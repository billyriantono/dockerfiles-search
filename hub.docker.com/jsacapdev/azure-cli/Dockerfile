FROM microsoft/dotnet:2.1-sdk

RUN apt-get update \
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli stretch main" > /etc/apt/sources.list.d/azure-cli.list' \
    && apt-get install -y --no-install-recommends \
        apt-transport-https \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        azure-cli 

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        apt-transport-https \
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list' \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        powershell=6.0.0-1.debian.9 \
    && rm -rf /var/lib/apt/lists/*

CMD [ "pwsh" ]