FROM thedrhax/jenkins-slave-alpine

MAINTAINER Dmitry Karikh <the.dr.hax@gmail.com>

# Docker & Rancher settings
ENV DOCKER_HUB_LOGIN="dXNlcm5hbWU6cGFzc3dvcmQ=" \
    DOCKER_HUB_EMAIL="example@example.com" \
    RANCHER_URL="http://server_ip:8080/" \
    RANCHER_ACCESS_KEY="" \
    RANCHER_SECRET_KEY=""

# Install Docker client
RUN apk --no-cache add docker

# Install rancher-compose
RUN wget -O /tmp/rc.tgz https://github.com/rancher/rancher-compose/releases/download/v0.12.5/rancher-compose-linux-amd64-v0.12.5.tar.gz > /tmp/rc.tgz \
 && tar -xzvf /tmp/rc.tgz \
 && mv rancher-compose-v0.12.5/rancher-compose usr/bin \
 && rm -rf rancher-compose-v0.12.5 \
 && rm /tmp/rc.tgz

# Include required scripts
ADD prepare-docker.sh /entrypoint.d/
