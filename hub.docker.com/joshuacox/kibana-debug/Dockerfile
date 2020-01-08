FROM docker.elastic.co/kibana/kibana:5.5.0
USER root

RUN yum update -y \
  && yum install -y \
    wget bind-utils nmap curl mtr traceroute \
  && yum clean all

USER kibana
