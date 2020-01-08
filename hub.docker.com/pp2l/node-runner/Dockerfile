FROM node:5.11.0

RUN mkdir -p /opt/src
VOLUME /opt/src

ADD bin/node-entry /usr/bin/node-entry

WORKDIR /opt/src
ENTRYPOINT ["node-entry"]
