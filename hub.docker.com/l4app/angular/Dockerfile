FROM alexsuch/angular-cli:1.6.3

LABEL maintainer "grzegorz.lyskawa@l4a-soft.com"

RUN apk update
RUN apk add firefox-esr dbus xvfb
RUN Xvfb :99 &
RUN export DISPLAY=:99
