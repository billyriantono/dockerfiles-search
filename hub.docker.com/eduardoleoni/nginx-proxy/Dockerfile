FROM jwilder/nginx-proxy
RUN mkdir /etc/nginx/cache
RUN { \
      echo 'server_tokens off;'; \
      echo 'client_max_body_size 400m;'; \
    } > /etc/nginx/conf.d/my_proxy.conf

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log