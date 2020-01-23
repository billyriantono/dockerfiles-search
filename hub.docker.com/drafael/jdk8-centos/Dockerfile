FROM centos:7

LABEL maintainer="D.R4F4EL <d.r4f4el@gmail.com>"
LABEL version="Java (JDK) 1.8.0-openjdk, CentOS 7"

ENV JAVA_VERSION 1.8.0-openjdk
ENV GOSU_VERSION 1.10

RUN set -ex; yum -y update; \
  \
# install java
  yum -y install java-${JAVA_VERSION}-devel; \
  \
# grab gosu for easy step-down from root
  yum -y install epel-release; \
  yum -y install wget dpkg; \
  \
  dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')"; \
  wget -O /usr/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch"; \
  wget -O /tmp/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch.asc"; \
  \
# verify the signature
  export GNUPGHOME="$(mktemp -d)"; \
  gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4; \
  gpg --batch --verify /tmp/gosu.asc /usr/bin/gosu; \
  rm -r "$GNUPGHOME" /tmp/gosu.asc; \
  \
  chmod +x /usr/bin/gosu; \
# verify that the binary works
  gosu nobody true; \
  \
# cleanup
  yum -y remove wget dpkg; \
  yum clean all
