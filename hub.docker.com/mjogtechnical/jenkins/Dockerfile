FROM jenkins/jenkins:lts

USER root

RUN set -x \
  && apt-get update \
  && apt-get install -y \
    ghostscript

RUN ln -sf /usr/lib/libgs.so.9 /usr/lib/libgs.so
RUN wget -qO- https://download.docker.com/linux/static/stable/x86_64/docker-17.12.0-ce.tgz | tar -xzf- && cp ./docker/docker /usr/bin/docker && chmod +x /usr/bin/docker
RUN wget -O /usr/bin/jq https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 && chmod +x /usr/bin/jq

USER jenkins
