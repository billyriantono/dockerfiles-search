FROM nginx

# this file writing won't work after declaring a volume for this path
RUN { \
      echo 'proxy_connect_timeout 10m;'; \
      echo 'proxy_send_timeout 10m;'; \
      echo 'proxy_read_timeout 10m;'; \
      echo 'send_timeout 10m;'; \
      echo 'client_max_body_size 100m;'; \
    } > /etc/nginx/conf.d/extended_timeouts.conf

VOLUME "/etc/nginx/conf.d"
VOLUME "/etc/nginx/vhost.d"
VOLUME "/usr/share/nginx/html"
VOLUME "/etc/nginx/certs"

COPY ./html /usr/share/nginx/html
