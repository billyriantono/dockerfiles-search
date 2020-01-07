FROM nginx:stable-alpine
MAINTAINER moomoo <moomoo@sk.com>

COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf
COPY html /usr/share/nginx/html

EXPOSE 80 8080 443 

CMD ["nginx", "-g", "daemon off;"]

