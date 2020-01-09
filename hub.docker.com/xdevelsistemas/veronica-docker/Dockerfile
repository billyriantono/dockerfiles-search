FROM centos:7
MAINTAINER Clayton Silva <clayton@xdevel.com.br>
MAINTAINER Pedro Nakibar <pedro.nakibar@xdevel.com.br>

ENV MESOS_VERSION=0.27.0


RUN rpm -i http://repos.mesosphere.io/el/7/noarch/RPMS/mesosphere-el-repo-7-1.noarch.rpm && yum -y install mesos-$MESOS_VERSION

ENTRYPOINT ["/usr/sbin/mesos-master"]

ENV MESOS_WORK_DIR /tmp/mesos

VOLUME /tmp/mesos
