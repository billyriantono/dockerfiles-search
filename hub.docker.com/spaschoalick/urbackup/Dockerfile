FROM centos:7
MAINTAINER Santiago Paschoalick <spaschoalic@hotmail.com>

RUN yum -y install wget nmap nano telnet sqlite3 libcrypto++6 libcurl3 libfuse2 && wget http://download.opensuse.org/repositories/home:uroni/CentOS_7/home:uroni.repo -P /etc/yum.repos.d 

RUN yum -y install urbackup-server

EXPOSE 55413/tcp 55414/tcp 55415/tcp 35623/udp

VOLUME [ "/backups", "/var/urbackup", "/var/log" ]

COPY START.sh /opt/START.sh
