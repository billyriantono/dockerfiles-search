FROM alpine:3.3

RUN apk add --no-cache --repository http://pub.ixbox.jp/alpine/v3.3/main/ --allow-untrusted nginx-lua \
      && ln -sf /dev/stdout /var/log/nginx/access.log \
      && ln -sf /dev/stderr /var/log/nginx/error.log

CMD ["nginx", "-g", "daemon off;"]
