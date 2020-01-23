# FROM openjdk:alpine
FROM alpine
MAINTAINER biboheart "biboheart@qq.com"

# 安装imagemagick & fontconfig 字体配置
RUN apk --update add openjdk8 && \
apk --update add imagemagick && \
apk --update add ffmpeg && \
apk --update add ttf-dejavu &&  \
rm -rf /tmp/* /var/cache/apk/*

# 拷贝字体文件
COPY fonts/simsun.ttc /usr/share/fonts/simsun.ttc

CMD [ "/bin/sh" ]
