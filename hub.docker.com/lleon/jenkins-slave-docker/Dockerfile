# This is an autogenrated file do not edit it directly
FROM jenkinsci/jnlp-slave:latest
USER root

ENV DOCKER_VERSION 1.13.1
RUN curl -fsSLO https://get.docker.com/builds/Linux/x86_64/docker-${DOCKER_VERSION}.tgz && tar --strip-components=1 -xvzf docker-${DOCKER_VERSION}.tgz -C /usr/bin


RUN apt-get update \
    && apt-get install -y --no-install-recommends git g++ build-essential netcat jq rsync \
    && rm -rf /var/lib/apt/lists/*


USER jenkins