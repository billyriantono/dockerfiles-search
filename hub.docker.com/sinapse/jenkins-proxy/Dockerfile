FROM node:8

RUN mkdir /jenkins-proxy

COPY *.js package.json /jenkins-proxy/

COPY src /jenkins-proxy/src

WORKDIR /jenkins-proxy

ENV JENKINS_URL=http://tools.develop.sinapse-ps.com:9000/buildByToken/buildWithParameters?token=fgQ0QWdAFR&job=board-orchestrator

RUN npm i && \
    npm i -g pm2

CMD pm2 start --no-daemon server.js
