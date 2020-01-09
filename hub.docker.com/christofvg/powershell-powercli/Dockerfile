FROM ubuntu:18.04

LABEL maintainer="Christof Van Geendertaelen <christof@groovesoundz.be>"

WORKDIR "/tmp"

ADD "https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb" /tmp/packages-microsoft-prod.deb

RUN apt-get update \
    && apt-get install -y /tmp/packages-microsoft-prod.deb \
    && apt-get update \
    && apt-get install -y powershell

RUN pwsh -NoLogo -NoProfile -Command "Install-Module -Name VMware.PowerCLI -Force"

CMD [ "pwsh" ]