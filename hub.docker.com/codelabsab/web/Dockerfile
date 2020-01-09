FROM gliderlabs/alpine
MAINTAINER CodeLabs <contact@codelabs.se>

RUN apk-install ca-certificates nginx curl && mkdir -p /usr/share/nginx/html/ /var/log/nginx/ /etc/nginx/cert/
COPY src/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]
