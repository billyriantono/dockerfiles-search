FROM jenkins:latest

ENV DOCKER_VERSION 1.6.2

USER root

# Let's start with some basic stuff.
RUN apt-get update && apt-get install -y --no-install-recommends \
        apt-transport-https \
        ca-certificates \
        lxc \
        iptables \
        apparmor

# Install docker, shoreman, gosu
RUN \
    echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9 && \
    apt-get update && apt-get install -y lxc-docker-$DOCKER_VERSION && rm -rf /var/lib/apt/lists/* && \
    wget https://github.com/hecticjeff/shoreman/raw/master/shoreman.sh -O /usr/local/bin/shoreman && \
    wget https://github.com/tianon/gosu/releases/download/1.4/gosu-amd64 -O /usr/local/bin/gosu && \
    chmod +x /usr/local/bin/shoreman /usr/local/bin/gosu && \
    usermod -a -G docker jenkins

COPY Procfile plugins.txt /
COPY wrapdocker plugins.sh /usr/local/bin/

# Install jenkins plugins
RUN /usr/local/bin/plugins.sh /plugins.txt

RUN sed -i '/find/achown -R jenkins:jenkins /var/jenkins_home' /usr/local/bin/jenkins.sh

VOLUME ["/var/jenkins_home", "/var/lib/docker"]

EXPOSE 8080 50000

CMD ["shoreman"]

