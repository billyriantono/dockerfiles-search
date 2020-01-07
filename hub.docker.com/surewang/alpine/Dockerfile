FROM alpine
LABEL maintainer="surewang, 885374150@nwsuaf.edu.cn"

ENV APK_MIRRORS='https://mirrors.cloud.tencent.com/alpine'

COPY ./.vimrc /root/

RUN sed -i "s#http.*alpine#$APK_MIRRORS#g" /etc/apk/repositories \
        && apk update \
        && apk add --no-cache vim
