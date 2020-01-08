FROM centos:centos6
MAINTAINER Daniel Kang <me@daniel.gs>

COPY ./versions.json /versions.json

RUN yum -y install epel-release

RUN	yum -y install tar which jq npm && \
	npm install -g n@`jq -r .n /versions.json` && \
	n `jq -r .node /versions.json` && \
	npm install -g npm@`jq -r .npm /versions.json`

ENV NODE_PATH /usr/local/lib/node_modules

CMD ["node"]
