FROM alpine

ENV VNC_PASSWD="xvfb-firefox"
# 显示参数
ENV DISPLAY_WIDTH=1024
ENV DISPLAY_HEIGHT=768
ENV HOMEPAGE="https://www.baidu.com"

ENV HOME /home/alpine
# 设置为非交互式
ENV DEBIAN_FRONTEND noninteractive
# 设置 locale
ENV LC_ALL C.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

#设置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime


RUN echo "http://dl-3.alpinelinux.org/alpine/edge/testing" >>/etc/apk/repositories \
 && apk --no-cache add \
    x11vnc xvfb supervisor sudo \
    dwm dmenu ii st \
    ttf-ubuntu-font-family \
 && addgroup alpine \
 && adduser -G alpine -s /bin/ash -D alpine \
 && echo "alpine:alpine" | /usr/sbin/chpasswd \
 && mkdir -p /etc/supervisor/conf.d \
 && apk --no-cache add --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing firefox \
 && apk --no-cache add --repository http://nl.alpinelinux.org/alpine/edge/testing --allow-untrusted  wqy-zenhei

WORKDIR /home/alpine

# 拷贝 novnc 和 firefox 配置
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY noVNC-1.1.0 /home/alpine/novnc
COPY websockify-0.8.0 /home/alpine/novnc/utils/websockify
COPY mozilla /home/alpine/.mozilla
COPY cache /home/alpine/.cache

# 导出端口
EXPOSE 5900
EXPOSE 8060
VOLUME /home/alpine/Downloads

RUN  rm -rf /apk /tmp/* /var/cache/apk/* \
 && mkdir -p /home/alpine/.vnc \
 && chown -R alpine:alpine /home/alpine 

USER alpine
CMD ["/usr/bin/supervisord","-c","/etc/supervisor/conf.d/supervisord.conf"]