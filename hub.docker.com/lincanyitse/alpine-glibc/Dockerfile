FROM alpine
ENV GLIBC_VER '2.29-r0'
RUN set -x \
    && sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk add -q --no-cache --upgrade busybox bash bash-doc bash-completion wget curl vim tzdata ttf-dejavu fontconfig \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo Asia/Shanghai > /etc/timezone \
    && wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
    && wget -nv -O /tmp/glibc-${GLIBC_VER}.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VER}/glibc-${GLIBC_VER}.apk \
    && wget -nv -O /tmp/glibc-bin-${GLIBC_VER}.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VER}/glibc-bin-${GLIBC_VER}.apk \
    && wget -nv -O /tmp/glibc-i18n-${GLIBC_VER}.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VER}/glibc-i18n-${GLIBC_VER}.apk \
    && cd /tmp && apk add -q --no-cache glibc-${GLIBC_VER}.apk glibc-bin-${GLIBC_VER}.apk glibc-i18n-${GLIBC_VER}.apk \
    && echo -e "en_AG\nen_AU\nen_BW\nen_CA\nen_DK\nen_GB\nen_HK\nen_IE\nen_IN\nen_NG\nen_NZ\nen_PH\nen_SG\nen_US\nen_ZA\nen_ZM\nen_ZW\nzh_CN\nzh_HK\nzh_SG\nzh_TW\nzu_ZA" >/tmp/locale.md \
    && cat locale.md | xargs -i /usr/glibc-compat/bin/localedef -i {} -f UTF-8 {}.UTF-8 \
    && apk del -q tzdata wget && rm -rf /tmp/* /var/cache/apk/* /etc/apk/keys/sgerrand.rsa.pub \
    && sed -i 's/ash/bash/g' /etc/passwd

COPY .bashrc /root/.bashrc