FROM centos:6

MAINTAINER Stanly Xiang <stanly.sxiang@gmail.com>

# install document with yum
RUN sed -i 's/tsflags=nodocs//g' /etc/yum.conf

# install all software we need
RUN yum install -y epel-release && \
 yum makecache && \
 yum install -y man passwd sudo tar which git mlocate links make bzip2 \
 autoconf automake libtool m4 gcc gcc-c++ gdb flex cmake gperf indent unzip \
 libuuid-devel krb5-devel libgsasl-devel expat-devel libxml2-devel \
 perl-ExtUtils-Embed pam-devel python-devel snappy-devel \
 libyaml-devel libevent-devel bzip2-devel openssl-devel \
 openldap-devel readline-devel net-snmp-devel apr-devel \
 libesmtp-devel xerces-c-devel python-pip json-c-devel \
 apache-ivy java-1.7.0-openjdk-devel R-core-devel \
 openssh-clients openssh-server bison bison-devel libffi-devel \
 createrepo httpd perl rsync rpm-build vim wget python-setuptools \
 https://s3-us-west-2.amazonaws.com/pivotal-public/apache-maven-3.3.9-1.el6.noarch.rpm && \
 yum clean all

RUN cd /tmp; curl https://cmake.org/files/v3.1/cmake-3.1.0-Linux-x86_64.tar.gz -o cmake-3.1.0-Linux-x86_64.tar.gz && \
  tar xzvf cmake-3.1.0-Linux-x86_64.tar.gz && cd /tmp/cmake-3.1.0-Linux-x86_64 && sudo cp -rf * /usr/

# Install thirdparty dependency
RUN mkdir /hawqrepo && pushd /hawqrepo && \
    wget --quiet https://s3-us-west-2.amazonaws.com/pivotal-public/hdb-yum-2.1.0.0-1.tar.gz && \
    tar xfp ./*.tar.gz --strip-components=1 && \
    echo -e "[Thirdparty-deps]\nname=HAWQ Thirdparty dependencies\n"\
"baseurl=file:///hawqrepo/hawq\ngpgcheck=0\nenabled=1\npriority=1" > /etc/yum.repos.d/hawq_deps.repo && \
    rm *.tar.gz && popd && yum -y install thrift boost protobuf perl-JSON lcov libicu ldconfig

# Install apache maven
RUN curl -L "http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo" -o /etc/yum.repos.d/epel-apache-maven.repo && \
 yum install -y apache-maven && \
 yum clean all

RUN yum install -y mysql-server mysql-connector-java*
# Install python modules
RUN pip --retries=50 --timeout=300 install pg8000 simplejson unittest2 pycrypto pyyaml lockfile paramiko psi && \
  pip --retries=50 --timeout=300 install http://darcs.idyll.org/~t/projects/figleaf-0.6.1.tar.gz && \
  pip --retries=50 --timeout=300 install http://sourceforge.net/projects/pychecker/files/pychecker/0.8.19/pychecker-0.8.19.tar.gz/download

# Upgrade GCC
RUN cd /etc/yum.repos.d && curl https://people.centos.org/tru/devtools-2/devtools-2.repo -o devtools-2.repo
RUN yum install -y devtoolset-2-gcc devtoolset-2-binutils devtoolset-2-gcc-c++ || pwd
RUN scl enable devtoolset-2 bash && gcc --version
RUN echo "source /opt/rh/devtoolset-2/enable" >> /root/.bashrc

# setup ssh server and keys for root
RUN ssh-keygen -t rsa -N "" -f ~/.ssh/id_rsa && \
 cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
 chmod 0600 ~/.ssh/authorized_keys

# setup JAVA_HOME for all users
RUN echo "#!/bin/sh" > /etc/profile.d/java.sh && \
 echo "export JAVA_HOME=/etc/alternatives/java_sdk" >> /etc/profile.d/java.sh && \
 chmod a+x /etc/profile.d/java.sh

# Remove openjdk client folder
RUN sudo rm -rf /etc/alternatives/java_sdk/jre/lib/amd64/client

# install ec2-api-tools and set env
RUN cd /tmp;curl http://s3.amazonaws.com/ec2-downloads/ec2-api-tools.zip -o ec2-api-tools.zip && \
  unzip ec2-api-tools.zip && sudo mv ec2-api-tools-* /usr/local/bin/ec2-api-tools
ENV EC2_HOME /usr/local/bin/ec2-api-tools
ENV EC2_URL ec2.us-west-2.amazonaws.com
ENV JAVA_HOME /etc/alternatives/java_sdk
ENV M2_HOME=/usr/share/apache-maven
ENV MAVEN_OPTS="-Xmx2048m"
ENV PATH $EC2_HOME/bin/:$PATH
#install jq for json parse
RUN cd /tmp;curl http://stedolan.github.io/jq/download/linux64/jq -o jq && \
  chmod a+rx jq && sudo mv jq /usr/local/bin/
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:$M2_HOME/bin:$JAVA_HOME/bin:$PATH

# create user gpadmin since HAWQ cannot run under root
RUN groupadd -g 1000 gpadmin && \
 useradd -u 1000 -g 1000 gpadmin && \
 echo "gpadmin  ALL=(ALL)       NOPASSWD: ALL" > /etc/sudoers.d/gpadmin

# sudo should not require tty
RUN sed -i -e 's|Defaults    requiretty|#Defaults    requiretty|' /etc/sudoers

RUN echo "#!/bin/bash" > /etc/profile.d/user.sh && \
 echo "export USER=\`whoami\`" >> /etc/profile.d/user.sh && \
 chmod a+x /etc/profile.d/user.sh

RUN echo $'gpadmin soft nofile 2900000\n\
gpadmin hard nofile 2900000\n\
gpadmin soft nproc 131072\n\
gpadmin hard nproc 131072\n' \
 > /etc/security/limits.d/gpadmin.conf

ENV BASEDIR /data
RUN mkdir -p /data && chmod 777 /data

USER gpadmin

RUN echo "source /opt/rh/devtoolset-2/enable" >> ~/.bashrc
# setup ssh client keys for gpadmin
RUN ssh-keygen -t rsa -N "" -f ~/.ssh/id_rsa && \
 cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
 chmod 0600 ~/.ssh/authorized_keys

USER root

WORKDIR /data
