# Build using: docker build -f Dockerfile.gocd-agent -t gocd-agent .
FROM phusion/baseimage:0.9.16
MAINTAINER Ahmad Iqbal Ali <ahmad@aurorasolutions.io>

RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

#install utilities
RUN apt-get update && apt-get install -y -q unzip wget curl git

RUN mkdir /etc/service/go-agent
ADD gocd-agent/go-agent-start.sh /etc/service/go-agent/run

ADD http://download.go.cd/gocd-deb/go-agent-15.1.0-1863.deb /tmp/go-agent.deb

WORKDIR /tmp
RUN dpkg -i /tmp/go-agent.deb && \
    sed -i -e 's/DAEMON=Y/DAEMON=N/' /etc/default/go-agent /etc/default/go-agent
RUN curl -sSL https://get.docker.io/ubuntu/ | sh

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY docker /etc/default/docker
COPY sudoers /etc/sudoers.d/sudoers

CMD ["/sbin/my_init"]
