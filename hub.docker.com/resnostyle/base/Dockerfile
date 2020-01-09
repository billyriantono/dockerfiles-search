FROM centos:7
Maintainer Bryan Pearson <bwp.pearson@gmail.com>

RUN rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7 && \
     yum -y install epel-release && \
     yum upgrade -y && \
     yum clean all && \
     rm -rf /etc/ld.so.cache && \
     rm -rf /sbin/sln && \
     rm -rf /usr/{{lib,share}/locale,share/{man,doc,info,gnome/help,cracklib,il8n},{lib,lib64}/gconv,bin/localedef,sbin/build-locale-archive} && \
     rm -rf /var/cache/ldconfig/* && \
     rpmdb --rebuilddb; rpmdb --initdb
