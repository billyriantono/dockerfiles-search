FROM centos:6

COPY installers/ /root/

# install and enable required repositories and build tools
RUN /root/yum/install.sh

# install lighttpd
RUN /root/lighttpd/install.sh

# install mysql seerver and client
RUN /root/mysql/install.sh

# install php, composer, and xdebug
RUN /root/php/install.sh
RUN /root/php/install_composer.sh

# install supervisord and configuration file
RUN /root/supervisord/install.sh

VOLUME ["/var/www/lighttpd"]

# webserver
EXPOSE 80
EXPOSE 443

# mysql
EXPOSE 3306

CMD ["supervisord", "-n"]
