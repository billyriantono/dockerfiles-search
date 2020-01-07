FROM nginx:latest

ENV NGINX_SOCKET_LOCATION=/tmp/app.sock \
 NGINX_WORKER_PROCESSES=4 \
 NGINX_USER=nobody \
 NGINX_GROUP=nogroup \
 NGINX_WORKER_CONNECTIONS=1024 \
 NGINX_PORT=80 \
 NGINX_TIMEOUT=300 \
 NGINX_ACCEPT_MUTEX=on \
 NGINX_SENDFILE=on \
 NGINX_CLIENT_MAX_BODY_SIZE=4G 

COPY ./nginx.template /etc/nginx/nginx.template

CMD \
 envsubst '$$NGINX_WORKER_PROCESSES \
          $$NGINX_USER \
          $$NGINX_GROUP \
          $$NGINX_WORKER_CONNECTIONS \
          $$NGINX_PORT \
          $$NGINX_TIMEOUT \
          $$NGINX_ACCEPT_MUTEX \
          $$NGINX_SENDFILE \
          $$NGINX_CLIENT_MAX_BODY_SIZE \
          $$NGINX_SOCKET_LOCATION' < /etc/nginx/nginx.template > /etc/nginx/nginx.conf && \
 nginx -g "daemon off;"
