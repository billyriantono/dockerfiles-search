FROM nginx
MAINTAINER Chris Johns <chris@ter0.net> @ter0

ADD etc /etc
ADD entrypoint.sh /opt/entrypoint.sh

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list.d/backports.list \
&& apt-get update \
&& apt-get install openssl cron -y \
&& apt-get install -y -t jessie-backports certbot \
&& ln -s /etc/nginx/sites-available/ter0.net.conf /etc/nginx/conf.d/ter0.net.conf \
&& chmod a+x /opt/entrypoint.sh

ENTRYPOINT ["/opt/entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]

