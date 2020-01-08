FROM centos:centos7
MAINTAINER https://m-ko-x.de Markus Kosmal <code@m-ko-x.de>

ADD src/epel7.repo /etc/yum.repos.d/epel7.repo
ADD src/datastax.repo /etc/yum.repos.d/datastax.repo

RUN yum install -y wget tar openssh-server openssh-clients supervisor dsc21 sysstat sudo which openssl hostname && \
	yum clean all && \
	wget --progress=dot:giga -O /tmp/jdk.rpm --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u20-b26/jdk-8u20-linux-x64.rpm" && \
	rpm -ivh /tmp/jdk.rpm && rm /tmp/jdk.rpm && \
	alternatives --install /usr/bin/java java /usr/java/default/bin/java 20000

ADD src/supervisord.conf /etc/supervisord.conf
RUN mkdir -p /var/log/supervisor

ADD src/start.sh /usr/local/bin/start

RUN rm -f /etc/security/limits.d/cassandra.conf
RUN sed -i s/jamm-0.2.6.jar/jamm-0.2.8.jar/ /usr/share/cassandra/cassandra.in.sh

EXPOSE 9160 9042

USER root
CMD start
