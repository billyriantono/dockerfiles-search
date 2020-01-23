FROM nginx:latest as NGINX

RUN apt-get update \
    && apt-get install -y openssl certbot python-certbot-nginx

COPY nginx/nginx.conf /etc/nginx/nginx.conf
COPY nginx/conf.d/*.conf /etc/nginx/conf.d/
COPY nginx/web /usr/share/web
COPY nginx/bin /root/bin
COPY nginx/cert /data/cert

RUN chmod +x /root/bin/*.sh

CMD /root/bin/init.sh