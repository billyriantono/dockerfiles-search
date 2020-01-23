FROM ubuntu

MAINTAINER Scott Algatt

RUN apt-get update \
    && apt-get install -y nginx libnginx-mod-http-lua libnginx-mod-http-subs-filter software-properties-common\
    && add-apt-repository -y universe \
    && add-apt-repository -y ppa:certbot/certbot \
    && apt-get update \
    && apt-get -y install certbot python-certbot-nginx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
COPY ./conf/nginx.conf /etc/nginx/nginx.conf
COPY ./conf/site.conf /etc/nginx/sites-available/default

EXPOSE 80
CMD ["nginx"]
