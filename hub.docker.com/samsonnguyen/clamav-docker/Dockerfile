FROM centos:centos7
RUN yum install -y epel-release
RUN yum install -y clamav
WORKDIR "/var/lib/clamav"
VOLUME "/var/lib/clamav"
ENTRYPOINT ["/bin/bash"]
