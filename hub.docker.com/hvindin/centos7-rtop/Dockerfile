FROM docker.io/centos:latest
COPY dumb-init /usr/bin/dumb-init
RUN yum fs filter languages en:US && yum fs filter documentation \
    && yum update "*" -y && yum install -y epel-release && yum install -y nodejs npm openssh-clients \
    && yum clean all -y && npm -g install rtop && chmod +x /usr/bin/dumb-init \
    && useradd rtop
USER rtop
LABEL base.os="centos7" base.version="7.3.1611" htop.version="0.4.2"
ENTRYPOINT ["/usr/bin/dumb-init","--","/usr/bin/rtop"]
