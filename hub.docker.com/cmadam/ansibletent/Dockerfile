# Photon OS image with Powershell modules for common cloud providers (Azure, VMware & AWS). 
# Includes new (pre-release version) Azure powershell modules (AZ).

FROM vmware/powerclicore as base

RUN pwsh -c "Set-PSRepository -Name PSGallery -InstallationPolicy Trusted" && \
pwsh -c "\$ProgressPreference = \"SilentlyContinue\"; Install-Module -Name Az -AllowPrerelease" && \
pwsh -c "\$ProgressPreference = \"SilentlyContinue\"; Install-Module -Name AWSPowerShell.NetCore"

RUN mkdir -p /scripts

WORKDIR /scripts

LABEL maintainer="Andrew Clure" \
    description="This Dockerfile will install powershell modules for common cloud patforms (AWS, Azure & VMware)."

CMD [ "pwsh" ]
