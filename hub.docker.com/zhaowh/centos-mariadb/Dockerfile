FROM zhaowh/centos
MAINTAINER Zhao Weihong

# Install MariaDB.
RUN echo -ne " \
[mariadb] \n \
name = MariaDB \n \
baseurl = http://mirrors.aliyun.com/mariadb/yum/10.0/centos6-amd64 \n \
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB \n \
gpgcheck=0 \n \
" >  /etc/yum.repos.d/MariaDB.repo  && \
    yum update -y && \ 
    yum install -y pwgen MariaDB-server MariaDB-client  && \
    yum clean all && \
    rm -rf /var/lib/mysql/*

ADD assets/start.sh start.sh
RUN chmod 775 /*.sh


VOLUME ["/var/lib/mysql"]

EXPOSE 3306

CMD ["/start.sh"]
