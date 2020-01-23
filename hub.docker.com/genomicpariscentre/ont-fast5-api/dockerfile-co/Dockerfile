FROM node:6.3.0-slim
MAINTAINER Genevera <genevera.codes@gmail.com> (@genevera)

ENV ESDUMP_VERSION=3.1.0
RUN npm install -g elasticdump@${ES_DUMP_VERSION}

ENTRYPOINT ["/usr/local/bin/elasticdump"]
