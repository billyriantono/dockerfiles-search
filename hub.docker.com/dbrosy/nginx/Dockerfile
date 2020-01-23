FROM alpine:3.6

RUN apk add --update nginx && rm -rf /var/cache/apk/*

COPY nginx.non-root.conf /etc/nginx/nginx.conf
COPY index.html /usr/share/nginx/html/index.html

USER nobody

CMD ["nginx", "-g", "daemon off;"]
