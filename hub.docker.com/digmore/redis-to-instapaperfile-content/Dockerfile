FROM jenkins:2.7.2
USER root
RUN apt-get update
RUN apt-get install -y apt-transport-https ca-certificates
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo "deb https://apt.dockerproject.org/repo debian-jessie main" >> /etc/apt/sources.list.d/docker.list
RUN apt-get update
RUN apt-get install -y docker-engine
# RANCHER
ADD https://github.com/rancher/cli/releases/download/v0.1.0-rc3/rancher-linux-amd64-v0.1.0-rc3.tar.gz /usr/share/rancher-linux-amd64-v0.1.0-rc3.tar.gz
RUN tar xvf /usr/share/rancher-linux-amd64-v0.1.0-rc3.tar.gz --strip 2 -C /usr/local/bin
RUN chmod +x /usr/local/bin/rancher
