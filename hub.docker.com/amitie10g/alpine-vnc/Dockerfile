FROM lsiobase/alpine:3.10
MAINTAINER Davod
RUN apk --update --no-cache add \
         supervisor \
         dbus \
         xvfb \
         openbox \
         xterm \
         x11vnc \
         leafpad \
         pcmanfm \
         mesa-gles \
         mesa-egl \
         ttf-freefont \
         lynx \
         midori \
    && rm -rf /tmp/* /var/cache/apk/*
ADD root/ /
VOLUME /config
WORKDIR /config
EXPOSE 5900
