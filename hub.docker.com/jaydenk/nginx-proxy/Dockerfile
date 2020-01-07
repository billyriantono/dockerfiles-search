FROM jwilder/nginx-proxy:alpine
RUN { \
      echo 'server_tokens off;'; \
      echo 'client_max_body_size 50m;'; \
    } > /etc/nginx/conf.d/custom_proxy.conf
