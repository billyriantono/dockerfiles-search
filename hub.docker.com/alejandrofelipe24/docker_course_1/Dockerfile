FROM library/debian:jessie
MAINTAINER xmariachi@gmail.com
RUN apt-get update &&  \
        apt-get -y install apache2 && \ 
        apt-get -y install curl  && \ 
        apt-get -y install libapache2-mod-php5 php5-mysql php5-gd  && \
        a2enmod rewrite  && \
        a2enmod headers  && \
        a2enmod ssl  && \
	a2dismod status && \
	ln -sf /proc/self/fd/1 /var/log/apache2/access.log && \
	ln -sf /proc/self/fd/1 /var/log/apache2/error.log
ENTRYPOINT [ "/usr/sbin/apachectl" ,"-DFOREGROUND" ]
EXPOSE 22 80 443 

