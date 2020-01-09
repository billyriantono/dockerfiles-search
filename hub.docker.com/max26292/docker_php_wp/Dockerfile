FROM ubuntu:16.04
#setting Enviroment



ENV LANGUAGE       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8
ENV HOME /root
ENV DEBIAN_FRONTEND="noninteractive"
ENV MYSQL_USER=mysql \
    MYSQL_VERSION=5.7.22 \
    MYSQL_DATA_DIR=/var/lib/mysql \
    MYSQL_RUN_DIR=/run/mysqld \
    MYSQL_LOG_DIR=/var/log/mysql
# Init ubuntu to install some shits
RUN apt-get update
RUN apt-get clean && apt-get update && apt-get install -y locales
RUN localedef -i en_US -f UTF-8 en_US.UTF-8
RUN locale-gen en_US.UTF-8
RUN   apt-get install -y apt-utils
RUN apt-get upgrade -y
RUN  apt-get install python-software-properties -y
RUN  apt-get install software-properties-common -y
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt-get update -y --fix-missing
# Install required tools
RUN   apt-get install -y vim curl 
#Install Php7.1

# 
RUN  apt-get update
RUN  apt-get install -y php7.1
RUN  apt-cache search php7*

#install apache
RUN apt-get install apache2 -y
#install mysql
RUN apt-get install mysql-server -y
#open required port 
EXPOSE 80
EXPOSE 3306
EXPOSE 443
#start up apache and mysql 
# CMD ["/bin/bash",'service mysql start']
# CMD ["bin/bash", "service apache2 start"]
# ENTRYPOINT ["apachectl", "-D FOREGROUND"]
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
CMD ["mysqld"]