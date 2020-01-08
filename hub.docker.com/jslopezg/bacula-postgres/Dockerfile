FROM centos:7

MAINTAINER "jslopezg" <jslopezg@gmail.com>
ENV BACULA_VERSION "9.4.2"
LABEL com.baculasystems.bacula.version="${BACULA_VERSION}"

# Install postgres repository

RUN rpm -Uvh https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm

RUN yum -q -y update && \
    yum -q -y install postgresql96 sudo

RUN sed -i -e "s/Defaults    requiretty.*/ #Defaults    requiretty/g" /etc/sudoers

# Install Webmin
RUN yum install -q -y --nogpgcheck http://prdownloads.sourceforge.net/webadmin/webmin-1.900-1.noarch.rpm 
RUN yum -q -y install perl perl-Net-SSLeay openssl perl-IO-Tty perl-Encode-Detect perl-DBI perl-Digest-MD5 perl-Sys-Syslog perl-DBD-Pg
## COPY BACULA-CONFIG-FILE(bacula-config-files-settings)

# Install Bacula repo key
RUN rpm --import https://www.bacula.org/downloads/Bacula-4096-Distribution-Verification-key.asc

#Install Baculum
RUN rpm --import http://bacula.org/downloads/baculum/baculum.pub
COPY configs/baculum.repo /etc/yum.repos.d
RUN yum install -q -y baculum-common baculum-api baculum-api-httpd baculum-web baculum-web-httpd
# Cleanup caches and repository information
RUN yum clean all

# Add and save a copy of the bconsole config file. We'll populate it first boot.  
COPY configs/bconsole.conf /root/bconsole.conf.orig

# Add and save a copy of the FD config file. We'll populate it first boot.
COPY configs/bacula-fd.conf /root/bacula-fd.conf.orig

# Add and save a copy of the SD config file. We'll populate it first boot.
COPY configs/bacula-sd.conf /root/bacula-sd.conf.orig

# Add and save a copy of the DIR config file. We'll populate it first boot.
COPY configs/bacula-dir.conf /root/bacula-dir.conf.orig


#VOLUME /opt/bacula

ADD scripts/run.sh /

RUN chmod +x /run.sh

ENTRYPOINT ["/run.sh"]

EXPOSE 9095 9096 9101 9102 9103 10000