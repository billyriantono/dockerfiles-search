FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade && apt-get install -y apt-transport-https ca-certificates curl software-properties-common
ADD assets build_assets
RUN cat build_assets/docker-apt-key.gpg | apt-key add -
RUN add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose
RUN apt-get update && apt-get install -y docker-ce git firefox xvfb nodejs build-essential