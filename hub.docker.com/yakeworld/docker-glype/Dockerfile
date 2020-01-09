FROM php:7.2.2-apache-stretch

MAINTAINER yakeworld@gmail.com 

RUN apt update \
    && apt -y --no-install-recommends install wget unzip \        
    && wget https://jaist.dl.sourceforge.net/project/glypeproxy/glype-1.1/web-proxy-glype-1.1.zip -O /tmp/glype.zip \
    && unzip /tmp/glype.zip -d /var/www/html/ \
    && cp -r /var/www/html/glype-1.1/upload/* /var/www/html \
    && cp -r /var/www/html/glype-1.1/extras/* /var/www/html \
    && rm -r /var/www/html/glype-1.1 \		
    && rm /tmp/*.zip \
	  && chown -R www-data:www-data /var/www/html 
