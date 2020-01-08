FROM centos:7.2.1511
MAINTAINER MWS.PO <mws.po@playtech.com>

RUN groupadd -r node && useradd -r -g node node

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 0.10.36

# Install midlleware
RUN yum install -y openssh-clients git wget bzip2 freetype fontconfig

# Superfix for FE tests :)
RUN unlink /etc/localtime && ln -s /usr/share/zoneinfo/Etc/GMT-2 /etc/localtime

# Install Node
RUN curl -SLO https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz \
	&& tar -xvf node-v${NODE_VERSION}-linux-x64.tar.gz -C /usr/local --strip-components=1 \
	&& rm -f node-v${NODE_VERSION}-linux-x64.tar.gz \
	&& ln -s /usr/local/bin/node /usr/local/bin/nodejs
	
CMD ["node"]
