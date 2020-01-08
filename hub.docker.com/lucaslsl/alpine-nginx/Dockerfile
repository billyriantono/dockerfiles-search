FROM alpine:3.3

RUN apk add --no-cache nginx && mkdir /tmp/nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]