FROM alpine:3.5
RUN apk update && apk add nginx && rm -rf /var/cache/apk/*
RUN mkdir -p /tmp/nginx/client-body

COPY nginx/nginx.conf /etc/nginx/nginx.conf
COPY nginx/default.conf /etc/nginx/conf.d/default.conf
COPY static /usr/share/nginx/html/

CMD ["nginx", "-g", "daemon off;"]
