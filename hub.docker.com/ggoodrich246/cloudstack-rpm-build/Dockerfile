FROM centos:7

COPY mysql-community.repo /etc/yum.repos.d/mysql-community.repo
RUN rpm --import http://repo.mysql.com/RPM-GPG-KEY-mysql

RUN yum groupinstall -y "Development Tools"
RUN yum install -y \
        java-1.8.0-openjdk-devel.x86_64 \
        genisoimage \
        mariadb \
        mariadb-server \
        ws-commons-util \
        MySQL-python \
        python-setuptools \
        createrepo \
        maven \
        wget \
        bzip2 \
        which
RUN yum install -y mysql-connector-python

RUN useradd -ms /bin/bash jenkins
