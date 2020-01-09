FROM nginx


RUN apt-get update && apt-get install -y openssl && \
rm -rf /var/lib/apt/lists/*

COPY entrypoint.sh /usr/bin/docker-entrypoint
COPY nginx.conf /etc/nginx/conf.d/default.conf

RUN chmod +x /usr/bin/docker-entrypoint


ENTRYPOINT ["docker-entrypoint"]

CMD ["nginx", "-g", "daemon off;"]
