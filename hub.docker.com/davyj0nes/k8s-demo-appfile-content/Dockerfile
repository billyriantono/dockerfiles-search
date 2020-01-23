FROM node:8-stretch


RUN apt-get update \
    && apt-get install -y python3 python3-dev python3-pip zip groff \ 
    && apt-get clean && rm -rf /var/cache/apt/* && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

COPY install_python.sh /tmp/
RUN sh /tmp/install_python.sh

COPY install_aws.sh /tmp/
RUN sh /tmp/install_aws.sh

COPY install_docker.sh /tmp/
RUN sh /tmp/install_docker.sh
VOLUME /var/lib/docker

WORKDIR /root

ARG version=latest

WORKDIR /home/theia
ADD $version.package.json ./package.json
ARG GITHUB_TOKEN
RUN yarn --cache-folder ./ycache && rm -rf ./ycache
RUN yarn theia build
EXPOSE 3000
ENV SHELL /bin/bash
ENTRYPOINT [ "yarn", "theia", "start", "/home/project", "--hostname=0.0.0.0" ]
