FROM centos:5

RUN sed -i 's/enabled=1/enabled=0/' /etc/yum/pluginconf.d/fastestmirror.conf \
  && sed -i 's/mirrorlist/#mirrorlist/' /etc/yum.repos.d/*.repo \
  && sed -i 's|#baseurl=http://mirror.centos.org/centos/$releasever|baseurl=http://vault.centos.org/5.11|' /etc/yum.repos.d/*.repo \
  && yum update -y \
  && yum clean all
