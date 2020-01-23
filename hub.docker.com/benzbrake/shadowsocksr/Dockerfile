FROM benzbrake/alpine
MAINTAINER Ryan Lieu <github-benzBrake@woai.ru>

ENV command=""
ADD entrypoint.sh /usr/bin/
RUN set -ex \
    && if [ $(wget -qO- ipinfo.io/country) == CN ]; then echo "http://mirrors.aliyun.com/alpine/latest-stable/main/" > /etc/apk/repositories ;fi \
    && apk --update add --no-cache su-exec libsodium py-pip \
    && adduser -S ssr \
    && pip --no-cache-dir install https://github.com/shadowsocksr-backup/shadowsocksr/archive/manyuser.zip \
    && chmod +x /usr/bin/entrypoint.sh
    
ENTRYPOINT ["entrypoint.sh"]