FROM centos:7.2.1511
MAINTAINER Rayson Zhu <vfreex@gmail.com>

RUN yum update -y && yum install -y openssh-server initscripts git
RUN curl -L https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64 -o /usr/local/sbin/gosu && \
  chmod 0755 /usr/local/sbin/gosu && \
  curl -L https://cdn.gogs.io/gogs_v0.9.13_linux_amd64.tar.gz -o /tmp/gogs_v0.9.13_linux_amd64.tar.gz && \
  cd /opt && tar -xzvf /tmp/gogs_v0.9.13_linux_amd64.tar.gz && rm -f /tmp/gogs_v0.9.13_linux_amd64.tar.gz

ENV GOGS_CUSTOM /data/gogs
WORKDIR /opt/gogs
CMD ["gogs", "web"]
ENTRYPOINT ["/docker/docker-entrypoint.sh"]
EXPOSE 3000 22

# initialize
RUN mkdir -p /data && useradd git -d /data/git -s /bin/bash && passwd -u git -f

COPY files/ /

