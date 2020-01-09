FROM atlassian/bamboo-server

USER root

ENV DOCKER_ROOT_GROUP_ID=65536

# Install docker
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
RUN apt-key fingerprint 0EBFCD88I

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y docker-ce docker-ce-cli containerd.io

# Set docker socket permission

RUN touch /var/run/docker.sock

RUN groupadd dockerroot -g ${DOCKER_ROOT_GROUP_ID} && \
    usermod -a -G dockerroot ${BAMBOO_USER}
RUN chgrp dockerroot ${BAMBOO_SERVER_INSTALL_DIR} && \
    chgrp dockerroot /var/run/docker.sock
