FROM centos:centos6
MAINTAINER "Krzysztof Pawlowski" <msciciel@msciciel.eu>
RUN curl -L http://bootstrap.saltstack.com > salt.sh ; sh salt.sh -M -X; yum clean all
RUN yum install -y vim; yum clean all
ADD prompt.sh /etc/profile.d/
