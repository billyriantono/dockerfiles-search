FROM centos:7
ENV container docker
RUN yum install -y rsyslog; \
yum clean all
COPY . /
ENTRYPOINT ["/startrsyslogd.sh"]
