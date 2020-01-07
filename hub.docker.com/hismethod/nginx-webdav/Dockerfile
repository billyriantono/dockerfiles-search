FROM ubuntu:18.04
LABEL maintainer="JUNGMIN MOON <his.methods@gmail.com>"
RUN apt update && apt install -y nginx-extras apache2-utils

VOLUME /webdav
EXPOSE 443
COPY webdav.conf /etc/nginx/conf.d/default.conf
RUN rm -rf /etc/nginx/sites-enabled/*

COPY entrypoint.sh /var
WORKDIR /var
RUN chmod +x entrypoint.sh

CMD ./entrypoint.sh && nginx -g "daemon off;"