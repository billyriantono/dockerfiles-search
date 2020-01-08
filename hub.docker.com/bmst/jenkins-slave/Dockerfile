# Optimized by docker-optimize: https://www.npmjs.com/package/docker-optimize
FROM ubuntu:16.04
MAINTAINER Bogdan Mustiata <bogdan.mustiata@gmail.com>
ENV { "LANG":"en_US.UTF-8","LANGUAGE":"en_US:en","LC_ALL":"en_US.UTF-8" }
EXPOSE 22
CMD /usr/sbin/sshd -D
RUN locale-gen en_US.UTF-8 &&     apt-get update -y &&     DEBIAN_FRONTEND="noninteractive" apt-get upgrade -y &&     DEBIAN_FRONTEND="noninteractive" apt-get install -y openssh-server &&     sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd &&     mkdir -p /var/run/sshd && apt-get update -y &&     DEBIAN_FRONTEND="noninteractive" apt-get install -y openjdk-8-jre-headless && DEBIAN_FRONTEND="noninteractive" apt-get install -y wget git mercurial zip graphviz && useradd -m -d /home/jenkins -s /bin/sh jenkins &&     echo "jenkins:jenkins" | chpasswd && wget -O - https://get.docker.com | sh && echo 'DOCKER_OPTS="-H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock"' >> /etc/default/docker && usermod -G docker jenkins && apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin
