FROM docker.io/centos:latest
COPY dumb-init /usr/bin/dumb-init
RUN yum fs filter languages en:US && yum fs filter documentation \
    && yum install -y nmap && yum clean all -y && chmod +x /usr/bin/dumb-init \
    && adduser --uid 910 -d /home/nmap nmap
LABEL base.os="centos7" base.version="7.3.1611" nmap.version="6.40"
USER nmap
ENTRYPOINT ["/usr/bin/dumb-init","--","/usr/bin/nmap"]
