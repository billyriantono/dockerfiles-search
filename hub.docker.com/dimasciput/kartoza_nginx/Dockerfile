FROM nginx

ADD default.conf /etc/nginx/conf.d/default.conf
ARG SERVER_NAME=default

ADD update-nginx-conf.sh /update-nginx-conf.sh
RUN chmod +x /update-nginx-conf.sh
