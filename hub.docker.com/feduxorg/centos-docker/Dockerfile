FROM feduxorg/centos:latest
MAINTAINER dev@fedux.org

# ENV http_proxy http://172.17.42.1:3128
# ENV https_proxy https://172.17.42.1:3128

ADD docker.service /etc/systemd/system/docker.service
ADD docker.repo /etc/yum.repos.d/docker.repo

RUN curl "https://raw.githubusercontent.com/docker/docker/master/hack/dind" -o /usr/local/bin/dind \
  && chmod +x /usr/local/bin/dind

# Install docker
RUN yum install -y docker-engine \
  && systemctl enable docker

# Install docker compose
RUN yum install -y wget \
  && curl -s -L https://github.com/docker/compose/releases/latest \
  | egrep -o '/docker/compose/releases/download/[0-9.]*/docker-compose-Linux-x86_64' \
  | wget --base=http://github.com/ -i - -O /usr/local/bin/docker-compose \
  && chmod +x /usr/local/bin/docker-compose \
  && yum remove -y wget \
  && yum clean -y all


VOLUME ["/var/lib/docker"]
