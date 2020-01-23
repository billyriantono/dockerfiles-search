# use small node image
FROM debian:stretch-slim

RUN apt update \
&& apt-get install -y git openssh-client ca-certificates openssl jq gettext xmlstarlet curl wget xz-utils \
&& wget https://developer.salesforce.com/media/salesforce-cli/sfdx-linux-amd64.tar.xz \
&& mkdir sfdx \
&& tar -xJf sfdx-linux-amd64.tar.xz -C sfdx --strip-components 1 \
&& ./sfdx/install
