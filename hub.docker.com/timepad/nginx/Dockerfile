# docker build -t timepad/nginx -f Dockerfile . && docker push timepad/nginx

FROM nginx:latest

COPY wait-for-it.sh /usr/local/bin/wait-for-it
COPY envsubst.sh /usr/local/bin/nginx_envsubst

COPY docker.nginx /etc/nginx/nginx.conf
