FROM alpine:latest

MAINTAINER Laurent Smits "https://bitbucket.org/laurentsmits/alpine-xwine"

LABEL description="Minimal alpine xserver - wine 2.0"

#Upgrade Alpine linux
RUN apk update upgrade

#APK Local
ADD ./apk /apk
RUN cp /apk/.abuild/-58b83ac3.rsa.pub /etc/apk/keys
RUN apk --no-cache --update add /apk/x11vnc-0.9.13-r0.apk

#APK Community
RUN apk --no-cache add x11vnc xvfb openbox xfce4-terminal supervisor sudo alpine-base xvfb ncurses curl wine zenity

#APK Testing
RUN apk --no-cache add --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing winetricks mono

#Create alpine group ad user
RUN addgroup alpine \
  && adduser  -G alpine -s /bin/sh -D alpine \
  && echo "alpine:alpine" | /usr/sbin/chpasswd \
  && echo "alpine    ALL=(ALL) ALL" >> /etc/sudoers \
  && rm -rf /tmp/* /var/cache/apk/*

ADD ./etc /etc

ENV DISPLAY :0
ENV WINEPREFIX /home/alpine/.wine
ENV WINEARCH=win64

EXPOSE 5900

USER alpine

WORKDIR /home/alpine

CMD ["/usr/bin/supervisord","-c","/etc/supervisord.conf"]