FROM centos:7

RUN yum update -y

RUN yum -y groupinstall base "C Development Tools and Libraries" --setopt=group_package_types=mandatory,default,optional \
  && yum install -y wget mesa-libGL-devel \
  && rm -rf /var/cache/yum/* \
  && yum clean all

RUN wget http://download.qt.io/official_releases/qt/5.9/5.9.7/qt-opensource-linux-x64-5.9.7.run
