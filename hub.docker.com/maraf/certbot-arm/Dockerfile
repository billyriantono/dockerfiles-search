FROM ubuntu

RUN apt-get update -q && \
    apt-get install certbot -qy && \
    apt-get install nginx -qy

EXPOSE 80

ENTRYPOINT service nginx start && \
    certbot certonly --webroot -w /var/www/html/ -d $DOMAIN -m $EMAIL -n --agree-tos && \
    mkdir -p /mnt/certs && \
    cp -L /etc/letsencrypt/live/$DOMAIN/*.* /mnt/certs