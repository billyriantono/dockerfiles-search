FROM jpgo/jdk:oracle-1.8

MAINTAINER Jay Park Graven <jay.graven@cgifederal.com>

#ARG pass

#RUN cd /tmp \
# && debconf-set-selections << "mysql-server mysql-server/root_password password passwd" \
# && debconf-set-selections << "mysql-server mysql-server/root_password_again password passwd"

RUN export DEBIAN_FRONTEND=noninteractive && \
 apt-get update && \
 apt-get -y install adduser \
 curl \
 lsb-base \
 procps \
 zlib1g \
 gzip \
 python \
 python-support \
 sysstat \
 ntp bash tree \
 openssh-server \
 openssh-client \
 apt-transport-https \
 apache2 \
 php5 \
 libapache2-mod-php5 \
 php5-mcrypt \
 php5-curl \
 php5-mysql \
 php5-gd \
 php5-cli \
 php5-dev \
 mysql-client \
 mysql-server \
 libapache2-mod-auth-mysql \
 && php5enmod mcrypt \
 && mysql_install_db \
 && rm -rf /var/lib/apt/lists/*

RUN MIP=`ifconfig | sed -En 's/127.0.0.1//;s/.*inet (addr:)?(([0-9]*\.){3}[0-9]*).*/\2/p'` \
 && sed -i "s/bind_address/#bind_address/" /etc/ssh/sshd_config 
 
# apache
EXPOSE 80
# mysql 
EXPOSE 3306

#CMD /usr/bin/mysql_secure_installation
