FROM ubuntu:12.04
MAINTAINER bartojs

# upstart workaround
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN if [ -f /sbin/initctl ]; then mv /sbin/initctl /sbin/initctl-bakup; fi
RUN ln -s /bin/true /sbin/initctl

RUN echo 'deb http://archive.ubuntu.com/ubuntu precise main universe' > /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y nginx php5-fpm php5-mysql mysql-server openjdk-7-jre-headless vim curl zip
RUN rm /etc/nginx/nginx.conf /etc/nginx/sites-available/default /etc/php5/fpm/pool.d/www.conf 
ADD ./etc/php5/fpm/pool.d/www.conf /etc/php5/fpm/pool.d/www.conf  
ADD ./etc/nginx/sites-available/default /etc/nginx/sites-available/default
ADD ./etc/nginx/nginx.conf /etc/nginx/nginx.conf
ADD http://wordpress.org/latest.zip /usr/share/nginx/wordpress.zip
RUN /usr/bin/unzip /usr/share/nginx/wordpress.zip -d /usr/share/nginx/
RUN rm -fR /usr/share/nginx/www /usr/share/nginx/wordpress.zip
RUN mv /usr/share/nginx/wordpress /usr/share/nginx/www
ADD ./usr/share/nginx/www/wp-config.php /usr/share/nginx/www/wp-config.php
ADD ./usr/local/bin/docker-start.sh /usr/local/bin/docker-start.sh
RUN /usr/local/bin/docker-start.sh mysql

EXPOSE 80
CMD /usr/local/bin/docker-start.sh
