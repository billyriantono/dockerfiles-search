FROM registry.centos.org/centos/centos:7
MAINTAINER Jakub Rączkowski

LABEL name="karafior/nrpe" \
      description="Base NRPE image" \
      url="https://github.com/karafior"

RUN yum -y install epel-release && \
    yum -y install nrpe nagios-plugins-nrpe nagios-plugins-disk && \
    yum clean all

EXPOSE 5666

USER 998

ENTRYPOINT ["/usr/bin/bash", "-c"]
CMD ["/usr/sbin/nrpe $NRPE_SSL_OPT -c /etc/nagios/nrpe.cfg --no-forking"]
