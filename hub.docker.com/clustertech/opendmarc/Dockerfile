FROM centos:7
ENV container docker
RUN curl -Lo /tini https://github.com/krallin/tini/releases/download/v0.18.0/tini-amd64; \
chmod 755 /tini
RUN yum -y update; \
yum install -y epel-release rsyslog; \
yum install -y opendmarc; \
yum clean all; \
mv /etc/opendmarc.conf /etc/opendmarc/opendmarc.conf
COPY . /
ENTRYPOINT ["/tini", "/startopendmarc.sh"]
