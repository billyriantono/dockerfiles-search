FROM giabar/gb-c7sysd
MAINTAINER giabar
RUN yum -y install epel-release deltarpm &&\
    yum -y install wget tar curl zip unzip git
RUN yum -y install http://repos.mesosphere.io/el/7/noarch/RPMS/mesosphere-el-repo-7-1.noarch.rpm &&\
    yum -y install mesosphere-zookeeper mesos marathon chronos &&\
    echo 'docker,mesos' > /etc/mesos-slave/containerizers
ENV DOCKER_VERSION=1.13.0
RUN wget -q https://get.docker.com/builds/Linux/x86_64/docker-${DOCKER_VERSION}.tgz  && \
  tar xzf docker-${DOCKER_VERSION}.tgz && \
  mv docker/* /usr/bin/ && \
  chmod +x /usr/bin/docker && \
  rm -r docker*
RUN systemctl enable zookeeper &&\
    systemctl enable mesos-master &&\
    systemctl enable mesos-slave &&\
    systemctl enable marathon &&\
    systemctl enable chronos
#RUN systemctl restart docker &&\
#    systemctl restart zookeeper &&\
#    systemctl restart mesos-master &&\
#    systemctl restart mesos-slave &&\
#    systemctl restart marathon &&\
#    systemctl restart chronos
#RUN for SERVICES in docker zookeeper mesos-master mesos-slave marathon chronos; do systemctl enable $SERVICES && systemctl restart $SERVICES; done
CMD ["/usr/sbin/init"]
