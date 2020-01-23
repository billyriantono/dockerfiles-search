FROM alpine:3.5

EXPOSE 80

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG BUILD_DEPS=''
ARG RUN_DEPS='nginx openssl'

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
  && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

WORKDIR /etc/nginx

ADD . .

CMD ["nginx","-g","daemon off;"]
