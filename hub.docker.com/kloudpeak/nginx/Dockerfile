FROM kloudpeak/debian:latest
MAINTAINER Orkesh <orkesh@kloudpeak.com>
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62 && \
	echo "deb http://www.nginx.org/packages/debian/ wheezy nginx" > /etc/apt/sources.list.d/nginx.list && \
	apt-get update && \
	apt-get install -y nginx && \
	apt-get clean && \
	echo -n > /var/lib/apt/extended_states
VOLUME /etc/nginx/conf.d
VOLUME /etc/nginx/host.d
VOLUME /etc/nginx/nginx.d
VOLUME /data
RUN rm -rf /etc/nginx/*.d && \
	mkdir -p /etc/nginx/addon.d /etc/nginx/conf.d /etc/nginx/host.d /etc/nginx/nginx.d
ADD config /config
ADD etc /etc
ADD supervisord.conf /etc/supervisor/conf.d/nginx.conf
EXPOSE 80


#/data
#      /config
          # nginx-*.conf // included by nginx
          # php-*.conf // included by php5-fpm
      # /http
          # index.html // root web directory (index file is index.html or index.php)
      # /logs
          # nginx.log // nginx log file
          # php-fpm.log // php-fpm log file
      # /secure
          # filename.ext // private files such as passwords or keys