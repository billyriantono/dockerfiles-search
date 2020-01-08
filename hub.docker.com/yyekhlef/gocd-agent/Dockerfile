FROM centos:7
MAINTAINER "GoCD" <gocd-dev@googlegroups.com>
MAINTAINER Youcef Yekhlef <youcef.yekhlef@zenika.com>

ARG GO_VERSION="16.8.0-3929"
ARG DOWNLOAD_URL="https://download.go.cd/binaries"
ENV TINI_VERSION v0.9.0

RUN yum update -y && \
    yum install -y wget && \
    wget --no-cookies --no-check-certificate \
    --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
    "http://download.oracle.com/otn-pub/java/jdk/8u102-b14/jdk-8u102-linux-x64.rpm" && \
    yum localinstall -y jdk-8u102-linux-x64.rpm && \
    rm -f jdk-8u102-linux-x64.rpm && \
    yum clean all

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*; \
yum install -y java-1.8.0-openjdk-headless git;

VOLUME [ "/sys/fs/cgroup" ]

ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]


ADD $DOWNLOAD_URL/$GO_VERSION/rpm/go-agent-$GO_VERSION.noarch.rpm /tmp/go-agent.rpm

WORKDIR /tmp
RUN yum install -y /tmp/go-agent.rpm; yum clean all; rm -f /etc/default/go-server
ENV JAVA_HOME=/usr/lib/jvm/java-8-oracle/

# Run your program under Tini
CMD PRODUCTION_MODE=N /usr/share/go-agent/agent.sh

