# Based on https://github.com/evarga/docker-images/blob/master/jenkins-slave/Dockerfile

FROM debian:jessie
MAINTAINER Krzysztof Sinica <krzysztof.sinica@gmail.com>

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN echo "deb http://http.debian.net/debian jessie-backports main" >> /etc/apt/sources.list \
 && apt-get update \
 && apt-get install -y --no-install-recommends curl build-essential openjdk-8-jre-headless locales openssh-server \
 && locale-gen en_US.UTF-8 \
 && apt-get -q autoremove \
 && apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin \
 && sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd \
 && mkdir -p /var/run/sshd \
 && useradd -m -d /home/jenkins -s /bin/sh jenkins \
 && echo "jenkins:jenkins" | chpasswd \
 && curl -fsSL https://get.docker.com/ | sh
 
EXPOSE 22 
 
CMD ["/usr/sbin/sshd", "-D"]