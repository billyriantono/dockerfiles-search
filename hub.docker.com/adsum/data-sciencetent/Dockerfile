FROM ubuntu:14.04
MAINTAINER Adam Jimenez <adam.jimenez@gmail.com>

#RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y

#might need this
#RUN export DEBIAN_FRONTEND=noninteractive

RUN apt-get install -y openssh-server apache2 supervisor php5 php5-cli libapache2-mod-php5 php5-gd php5-json php5-ldap php5-mysql mariadb-server nano git curl php5-curl

RUN mkdir -p /var/run/sshd
RUN mkdir -p /var/log/supervisor

# mysql config
#ADD my.cnf /etc/mysql/conf.d/my.cnf
#RUN chmod 664 /etc/mysql/conf.d/my.cnf

RUN useradd ubuntu -d /home/ubuntu -s /bin/bash -m -U
RUN chown -R ubuntu:ubuntu /home/ubuntu
#RUN sudo adduser ubuntu sudo
#RUN echo ubuntu:ubuntu | chpasswd
RUN echo 'ubuntu ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/ubuntu
RUN chmod 0440 /etc/sudoers.d/ubuntu

RUN mkdir -p /home/ubuntu/workspace
ADD bashrc /home/ubuntu/.bashrc
ADD default_readme.md /home/ubuntu/workspace/README.md
ADD default_index.html /home/ubuntu/workspace/index.html
RUN chown -R ubuntu:ubuntu /home/ubuntu

RUN mkdir -p /home/ubuntu/.ssh
ADD ssh_config /home/ubuntu/.ssh/config
RUN chown -R ubuntu:ubuntu /home/ubuntu/.ssh
RUN chmod -R 700 /home/ubuntu/.ssh

ADD apache_default /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite
RUN sed -ri 's/^display_errors\s*=\s*Off/display_errors = On/g' /etc/php5/apache2/php.ini
RUN sed -ri 's/^display_errors\s*=\s*Off/display_errors = On/g' /etc/php5/cli/php.ini
RUN sed -ri 's/^error_reporting\s*=.*$/error_reporting = E_ALL \& ~E_DEPRECATED \& ~E_NOTICE/g' /etc/php5/apache2/php.ini
RUN sed -ri 's/^error_reporting\s*=.*$/error_reporting = E_ALL \& ~E_DEPRECATED \& ~E_NOTICE/g' /etc/php5/cli/php.ini
#RUN sed -ri 's/^PermitRootLogin.*$/PermitRootLogin yes/g' /etc/ssh/sshd_config

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD run /usr/local/bin/
RUN chmod +x /usr/local/bin/run

# Define mountable directories.
VOLUME ["/etc/mysql", "/var/lib/mysql", "/home/ubuntu/workspace"]

CMD ["/usr/local/bin/run"]
EXPOSE 80 22
