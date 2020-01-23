# Dockerfile for dvdstore/ds3

FROM centos/systemd

MAINTAINER Adam Robinson

#Add scripts that initialize the database
ADD content/ /

ENV container=docker

#Install all needed software
RUN yum -y install yum-utils && \
    yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum -y install https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm && \
    yum-config-manager --add-repo http://download.mono-project.com/repo/centos7/ && \
    rpm --import "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" && \
    yum -y install mysql-community-server mysql-community-client git redhat-lsb-core \
                   httpd php php-mysql expect openssh-server mono-complete && \
    yum -y update && yum clean all && \
    useradd -m web && chmod 755 /home/web/ && echo web | passwd --stdin web && \
    mkdir /root/mysql-connector && cd /root/mysql-connector && \
    curl -L -O https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9-noinstall.zip && \
    unzip mysql-connector-net-6.9.9-noinstall.zip && gacutil -i ./v4.0/MySql.Data.dll && \
    cd /root && git clone https://github.com/dvdstore/ds3.git && \
    rm -rf /root/ds3/ds3/oracleds3 && rm -rf /root/ds3/ds3/sqlserverds3 && \
    mkdir /var/www/html/ds3 && cp /root/ds3/ds3/mysqlds3/web/php5/* /var/www/html/ds3 && \
    sed -i '/^mysql\.default_user/ s/$/ web/' /etc/php.ini && \
    sed -i '/^mysql\.default_password/ s/$/ web/' /etc/php.ini && \
    cd /root/ds3/ds3/mysqlds3 && \
    csc /out:ds3mysqldriverNew.exe /root/ds3/ds3/drivers/ds3xdriver.cs /root/ds3/ds3/mysqlds3/ds3mysqlfns.cs \
        /d:GEN_PERF_CTRS /r:/root/mysql-connector/v4.0/MySql.Data.dll && \
    ln -s /usr/lib/systemd/system/httpd.service /etc/systemd/system/multi-user.target.wants/httpd.service && \
    ln -s /etc/systemd/system/createdb.service /etc/systemd/system/multi-user.target.wants/createdb.service && \
    rm -f /etc/systemd/system/multi-user.target.wants/mysqld.service

EXPOSE 80 3306

ENTRYPOINT ["/usr/sbin/init"]
