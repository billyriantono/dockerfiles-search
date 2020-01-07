FROM alpine:3.2

RUN apk add --update nginx && rm -rf /var/cache/apk/*

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
