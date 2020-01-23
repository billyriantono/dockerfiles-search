FROM centos:7
ENV container docker
RUN curl -Lo /tini https://github.com/krallin/tini/releases/download/v0.18.0/tini-amd64; \
chmod 755 /tini
RUN yum -y update; \
yum install -y cyrus-sasl cyrus-sasl-plain cyrus-sasl-ldap rsyslog; \
yum clean all; \
mkdir /etc/saslauthd; \
ln -s /etc/saslauthd/saslauthd.conf /etc/saslauthd.conf
COPY . /
ENTRYPOINT ["/tini", "/startsaslauthd.sh"]
