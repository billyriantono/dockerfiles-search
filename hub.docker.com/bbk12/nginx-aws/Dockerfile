FROM nginx:latest

ENV NGINX_AWS 0.7.4

ENV TERM xterm

RUN apt-get update && apt-get install -y \
        nano \
        wget \
        git 

ENV LOGPATH /var/log/nginx/healthd
RUN mkdir -p "$LOGPATH" && chmod -R 777 "$LOGPATH" && chown -R nginx:nginx "$LOGPATH"


RUN sed -i -e "s/worker_processes  1;/worker_processes  2;/g"  /etc/nginx/nginx.conf
RUN sed -i -e "s/worker_connections  1024;/worker_connections  2048;/g"  /etc/nginx/nginx.conf
RUN sed -i -e "s/pid        \/var\/run\/nginx.pid;/pid        \/var\/run\/nginx.pid;\nworker_rlimit_nofile 4096;/g" /etc/nginx/nginx.conf