FROM debian:jessie-slim
MAINTAINER openbee a.belhoula@openbee.com
#bash insted of sh
SHELL ["/bin/bash", "-c"]


RUN apt-get update && apt-get install -y  sed sudo ssh curl
#Openssl apache2 php5
RUN apt-get install openssl
RUN apt-get install -y libssl1.0.0
RUN apt-get install -y libssl-dev
RUN apt-get install -y php5 php5-mysql php-pear php5-ldap php5-curl php5-dev php5-apcu php5-gd php5-mcrypt
RUN apt-get install -y  apache2 libapache2-mod-python libapache2-mod-security2

ADD php-config.bash /php-config.bash
ADD apache-config.bash /apache-config.bash
ADD openbee.conf /etc/apache2/sites-available/openbee.conf
ADD openbee-ssl.conf /etc/apache2/sites-available/openbee-ssl.conf

RUN chmod 755 /php-config.bash
RUN chmod 755 /apache-config.bash
RUN /bin/bash /php-config.bash
RUN /bin/bash /apache-config.bash



#Rabbitmq server
RUN apt install -y rabbitmq-server
ADD rabbitmq.config /etc/rabbitmq/
ADD erlang.cookie /var/lib/rabbitmq/.erlang.cookie
ADD startrabbit.sh /opt/rabbit/
ADD startmysql.sh /opt/rabbit/
RUN chmod u+rw /etc/rabbitmq/rabbitmq.config \
&& chown rabbitmq:rabbitmq /var/lib/rabbitmq/.erlang.cookie \
&& chmod 400 /var/lib/rabbitmq/.erlang.cookie \
&& mkdir -p /opt/rabbit \
&& chmod a+x /opt/rabbit/startrabbit.sh

#Does NOT publish port, serves as documentation

EXPOSE 5672 
EXPOSE 5651
EXPOSE 15672

EXPOSE 80
EXPOSE 443

#mysql-community server 5.7.24
RUN apt update && apt install -y lsb-release wget debconf-utils
RUN wget https://dev.mysql.com/get/mysql-apt-config_0.8.7-1_all.deb
ADD sp.bash ./sp.bash
RUN chmod +777 ./sp.bash
RUN /bin/bash ./sp.bash
ADD my.cnf ./my.cnf
RUN rm -rf /var/lib/mysql &&\
    mkdir -p /var/lib/mysql /var/run/mysqld \
	&& chown -R mysql:mysql /var/lib/mysql /var/run/mysqld \
# ensure that /var/run/mysqld (used for socket and lock files) is writable regardless of the UID our mysqld instance ends up having at runtime
	&& chmod 777 /var/run/mysqld 
RUN cat ./my.cnf >> /etc/mysql/my.cnf
RUN chown -R mysql: /var/lib/mysql
EXPOSE 3306
EXPOSE 22 
#RUN service mysql restart
#RUN service mysql start
#RUN mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root -popenbee74
RUN chmod +x /opt/rabbit/startmysql.sh
#openbee portal repo
RUN echo "deb http://repodebian.myopenbee.com/openbee/ stable main" >> /etc/apt/sources.list
#entrypoint mysql
COPY startmysql.sh /usr/local/bin/
# backwards compat
RUN ln -s usr/local/bin/startmysql.sh /mysql.sh 


#Process Control System supervisor
RUN apt install -y supervisor
RUN echo "[supervisord]" > /etc/supervisord.conf && \
    echo "nodaemon=true" >> /etc/supervisord.conf && \
    echo "" >> /etc/supervisord.conf && \
    echo "[program:rabbitmq]" >> /etc/supervisord.conf && \
    echo "command=/opt/rabbit/startrabbit.sh" >> /etc/supervisord.conf && \
    echo "" >> /etc/supervisord.conf && \
    echo "[program:httpd]" >> /etc/supervisord.conf && \
    echo "command=/usr/sbin/apachectl -D FOREGROUND" >> /etc/supervisord.conf && \ 
    echo "" >> /etc/supervisord.conf && \
    echo "[program:mysql]" >> /etc/supervisord.conf && \
    echo "command=usr/local/bin/startmysql.sh" >> /etc/supervisord.conf && \
    echo "" >> /etc/supervisord.conf && \
    echo "[program:sshd]" >> /etc/supervisord.conf && \
    echo "command=service ssh start" >> /etc/supervisord.conf 
RUN sed -e 's/.*bind/#&/' -i /etc/mysql/mysql.conf.d/mysqld.cnf
RUN echo "root:openbee74" | chpasswd 
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config 
RUN service ssh restart
RUN apt install -y nano
#phpmyadmin
RUN echo "phpmyadmin phpmyadmin/internal/skip-preseed boolean true" | debconf-set-selections && \
        echo "phpmyadmin phpmyadmin/reconfigure-webserver multiselect apache2" | debconf-set-selections && \
         echo "phpmyadmin phpmyadmin/dbconfig-install boolean false" | debconf-set-selections
RUN apt-get -y install phpmyadmin
RUN service mysql start && \
                          mysql -uroot -popenbee74 -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'openbee74'" && \
                          mysql -uroot -popenbee74 -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'openbee74'" && \
                          mysql -uroot -popenbee74 -e "FLUSH PRIVILEGES" 
CMD ["/usr/bin/supervisord"]

