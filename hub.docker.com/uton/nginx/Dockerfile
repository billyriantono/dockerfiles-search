FROM danday74/nginx-lua
MAINTAINER BinarySoftware

COPY nginx.conf /nginx/conf/nginx.conf
COPY mime.types /nginx/conf/mime.types
RUN mkdir /nginx/ssl
COPY default.conf /nginx/conf/default.conf

EXPOSE 80 443

ENTRYPOINT ["nginx", "-g", "daemon off;"]