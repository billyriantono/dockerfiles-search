FROM centos:latest

VOLUME /build

RUN yum update -y
RUN yum install -y \
    curl

# Install Docker-Engine
RUN curl -sSL https://get.docker.com | sh
# Install Docker-Compose
RUN curl -L https://github.com/docker/compose/releases/download/VERSION_NUM/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

RUN useradd -g docker docker

USER docker
RUN /usr/local/bin/docker daemon -H tcp://0.0.0.0:2376

WORKDIR /build
ENTRYPOINT /usr/local/bin/docker-compose
CMD up
