# Originally forked from: git@github.com:gasi/docker-node-hello.git

FROM node:0.10

MAINTAINER Anna Doe <anna@example.com>

USER root

ENV AP /data/app
ENV SCPATH /etc/supervisor/conf.d


# Application Code
ADD *.js* $AP/

WORKDIR $AP

RUN npm install

EXPOSE 8080

CMD ["node", "index.js"]