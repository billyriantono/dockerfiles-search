FROM node:8-slim
RUN apt-get update \
  && apt-get install -y python-minimal make g++ git \
  && cd /tmp \
  && wget https://download.docker.com/linux/static/stable/x86_64/docker-17.09.1-ce.tgz \
  && tar -xvf docker*.tgz \
  && mv docker/docker /usr/local/bin \
  && rm -rf /tmp/*

