# a naive Redis image

# This shows systemd services (nginx and named) running in a centos7 container.
# There have been lots of problems and workarounds for this, see:
# https://hub.docker.com/_/centos/
# https://github.com/docker/docker/issues/7459

FROM centos
RUN yum -y update 
RUN yum install -y net-tools traceroute curl lynx telnet
