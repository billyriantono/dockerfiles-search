FROM debian:10

ENV CLIURL=https://developer.salesforce.com/media/salesforce-cli/sfdx-linux-amd64.tar.xz
ENV SFDX_AUTOUPDATE_DISABLE=false
ENV SFDX_USE_GENERIC_UNIX_KEYCHAIN=true
ENV SFDX_DOMAIN_RETRY=300
ENV SFDX_DISABLE_APP_HUB=true
ENV SFDX_LOG_LEVEL=DEBUG
ENV ROOTDIR=force-app/main/default/
ENV TESTLEVEL=RunLocalTests
ENV SCRATCH_ORG_ALIAS=DreamHouse_Scratch
ENV PACKAGEVERSION=""

ADD assets/server.key.enc /assets/

RUN apt-get update && apt-get -y install apt-utils openssl wget jq xz-utils && \
 openssl aes-256-cbc -d -md md5 -in /assets/server.key.enc -out assets/server.key -k Password01 && \
 mkdir sfdx && \
 wget -qO- $CLIURL | tar xJ -C sfdx --strip-components 1 && \
 "./sfdx/install" && \
 export PATH=./sfdx/$(pwd):$PATH && \
 sfdx --version && \
 sfdx plugins --core
