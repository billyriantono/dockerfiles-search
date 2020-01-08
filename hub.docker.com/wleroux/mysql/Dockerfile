FROM phusion/baseimage:0.9.13
MAINTAINER Wayne Leroux <WayneLeroux@gmail.com>

# Set up base image
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y dist-upgrade
ENV HOME /root
RUN echo 'LANG="en_EN.UTF-8"' > /etc/default/locale
CMD ["/sbin/my_init"]

# Support SSH
VOLUME /root/.ssh

# Install MySQL
RUN apt-get install -y mysql-server
RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/my.cnf
ADD init.sh /etc/my_init.d/mysql.sh
RUN mkdir /etc/service/mysql
ADD run.sh /etc/service/mysql/run
EXPOSE 3306
VOLUME /var/lib/mysql

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

