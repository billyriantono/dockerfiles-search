FROM centos:6

COPY inc.cnf /opt/

RUN yum -y install epel-release \
    yum -y install http://www.percona.com/downloads/percona-release/redhat/0.1-3/percona-release-0.1-3.noarch.rpm \
    && yum -y install wget python2-pip git gcc gcc-c++ make cmake bison openssl-devel ncurses-devel MySQL-python Percona-Server-client-56.x86_64  \
    && cd /opt \
    && git clone https://github.com/wowkingah/inception.git \
    && cd inception \
    && ./inception_build.sh debug \
    && mv /opt/inc.cnf /etc \
    && cd /opt \
    && yum -y install percona-toolkit.x86_64  \


EXPOSE 6669

ENTRYPOINT nohup /opt/inception/debug/mysql/bin/Inception --defaults-file=/etc/inc.cnf && bash