FROM amazonlinux:2016.09
MAINTAINER youyo

ENV SERVERLESS_VERSION=1.9.0
ENV SLS_IGNORE_WARNING=*
ENV PATH=/usr/local/node/bin:${PATH}

RUN yum install -y openssl curl git ca-certificates && \
	yum clean all && \
	git clone https://github.com/tagomoris/xbuild.git /usr/local/xbuild && \
	/usr/local/xbuild/node-install v7.7.3 /usr/local/node && \
	npm install -g serverless@${SERVERLESS_VERSION}
