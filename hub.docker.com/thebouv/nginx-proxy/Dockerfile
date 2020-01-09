FROM jwilder/nginx-proxy
RUN { \
      echo 'server_tokens off;'; \
      echo 'client_max_body_size 0;'; \
      echo 'add_header X-Frame-Options SAMEORIGIN;'; \
      echo 'add_header X-XSS-Protection "1; mode=block";'; \
    } > /etc/nginx/conf.d/my_proxy.conf
