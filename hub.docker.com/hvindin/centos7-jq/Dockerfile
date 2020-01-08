FROM docker.io/centos:latest
COPY dumb-init /usr/bin/dumb-init
RUN yum fs filter languages en:US && yum fs filter documentation \
    && yum install -y epel-release && yum install -y jq \
    && yum clean all -y && chmod +x /usr/bin/dumb-init
LABEL base.os="centos7" base.version="7.3.1611" jq.version="1.5"
ENTRYPOINT ["/usr/bin/dumb-init","--","/usr/bin/jq"]
CMD ["."]
