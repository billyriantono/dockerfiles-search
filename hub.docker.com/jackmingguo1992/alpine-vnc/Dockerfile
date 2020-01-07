FROM alpine:3.5
MAINTAINER Daniel Guerra
ADD /apk /apk
RUN cp /apk/.abuild/-58b83ac3.rsa.pub /etc/apk/keys
RUN apk --no-cache --update add /apk/x11vnc-0.9.13-r0.apk
RUN apk --no-cache add dbus firefox-esr
RUN apk add --update ttf-freefont
RUN apk --no-cache add xvfb openbox xfce4-terminal supervisor sudo \
&& addgroup alpine \
&& adduser  -G alpine -s /bin/sh -D alpine \
&& echo "alpine:alpine" | /usr/sbin/chpasswd \
&& echo "alpine    ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
&& rm -rf /apk /tmp/* /var/cache/apk/*
RUN echo '*/20 * * * * kill -9 `pgrep firefox`' > /var/spool/cron/crontabs/root
ADD etc /etc
WORKDIR /home/alpine
EXPOSE 5900
USER alpine
CMD ["sudo","/usr/bin/supervisord" ,"-c","/etc/supervisord.conf"]
