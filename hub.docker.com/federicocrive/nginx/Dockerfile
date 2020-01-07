FROM ubuntu:16.04
MAINTAINER Federico Crivellaro <crivellarofederico@gmail.com>

#Install Nginx

RUN apt-get update \
    && apt-get install -y \
    software-properties-common \
    iputils-ping \
    sudo \
    curl

RUN apt-add-repository -y ppa:nginx/stable

RUN apt-get update

RUN apt-get install -y nginx \
    && rm -rf /var/lib/apt/lists/*

ADD nginx/conf.d/nginx.conf /etc/nginx/nginx.conf
#ADD nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf

ADD data/www /data/www

RUN rm /etc/nginx/sites-enabled/default

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

RUN mkdir /etc/nginx/ssl/
COPY ./nginx/gls.key /etc/nginx/ssl/
COPY ./nginx/gls.crt /etc/nginx/ssl/


# testing
COPY ./data/www/tata.html /data/www/
COPY ./data/www/titi.html /data/www/

# CERTBOT 
#RUN apt-get update
#RUN apt-get install software-properties-common
#RUN add-apt-repository ppa:certbot/certbot -y
#RUN apt-get update
#RUN apt-get install python-certbot-nginx -y
#RUN certbot --nginx

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
