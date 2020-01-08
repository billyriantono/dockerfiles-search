FROM jenkins/jenkins
ARG DOCKER_CLIENT=docker-17.06.2-ce.tgz

USER root

RUN cd /tmp/ && curl -sSL -O https://download.docker.com/linux/static/stable/x86_64/${DOCKER_CLIENT} \
  && tar zxf ${DOCKER_CLIENT} \
  && mkdir -p /usr/local/bin \
  && mv ./docker/docker /usr/local/bin \
  && chmod +x /usr/local/bin/docker \
  && rm -rf /tmp/*

USER jenkins