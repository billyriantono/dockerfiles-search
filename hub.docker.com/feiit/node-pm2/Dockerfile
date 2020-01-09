FROM ubuntu:18.04

RUN apt-get -qq update && \
    apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs
RUN npm install pm2@latest -g
RUN adduser node
USER node

ENTRYPOINT ["pm2-docker", "ecosystem.config.js"]
