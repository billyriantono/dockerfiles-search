FROM nginx

ENV NGINX_UID 33
ENV NGINX_GID ${NGINX_UID}

RUN apt-get update && apt-get dist-upgrade -y
RUN apt-get install python3 python3-yaml -y

RUN mkdir -p /etc/nginx/locations.d
RUN mkdir -p /etc/nginx/proxy.d
RUN mkdir /docker-config

VOLUME /docker-config
VOLUME /var/cache/nginx

COPY nginx.conf /etc/nginx/nginx.conf

COPY server-gen.py /usr/local/bin/server-gen
RUN chmod +x /usr/local/bin/server-gen

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh

EXPOSE 80
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx"]
