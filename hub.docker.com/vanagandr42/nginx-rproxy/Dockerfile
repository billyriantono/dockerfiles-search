FROM vanagandr42/base:3.4-alpine-1.18.1.5

RUN apk upgrade --no-cache \
 && apk add --no-cache \
            nginx \
            openssl \
            certbot \

# Add cert renewal to crontab
 && crontab -l | { cat; echo "30 2 * * 1 /usr/bin/letsencrypt renew >> /var/log/nginx/le-renew.log"; \
                    echo "35 2 * * 1 /bin/s6-svscanctl -t /var/run/s6/services"; \
                    echo "";} | crontab - \
 
# Cleanup
 && rm -rf /var/log/nginx

# Declare volumes
VOLUME ["/opt/nginx-conf", \
        "/var/log/nginx", \
        "/etc/letsencrypt"]

# Add local files
COPY rootfs/ /

# Expose port of the webservice
EXPOSE 80/tcp \
       443/tcp