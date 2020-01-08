FROM himuradba/centos

#inception
RUN yum -y install wget git gcc gcc-c++ make cmake openssl-devel ncurses-devel m4\
    && cd /opt \
    && git clone https://github.com/himura-kenshin/inception.git \
    && rpm -i /opt/inception/dockersrc/bison-2.7-4.el7.x86_64.rpm \
    && mv /opt/inception/dockersrc/inc.cnf /etc \
    && cd /opt/inception \
    && ./inception_build.sh debug \
    && yum -y install https://repo.percona.com/yum/percona-release-latest.noarch.rpm \
    && yum -y install percona-toolkit \

#port
EXPOSE 3310

#start service
ENTRYPOINT nohup /opt/inception/debug/mysql/bin/Inception --defaults-file=/etc/inc.cnf && bash
