
# Adadted from Zenika/alpine-chrome
FROM python:2.7.15-alpine3.7

# Install chromium
RUN apk --update add \
    zlib \
    chromium \
    xvfb \
    wait4ports \
    xorg-server \
    dbus \
    ttf-freefont \
    mesa-dri-swrast \
    grep \ 
    udev \
    chromium-chromedriver

RUN pip install selenium nose names

ENV CHROME_BIN=/usr/bin/chromium-browser
ENV CHROME_PATH=/usr/lib/chromium/

CMD [ "/bin/sh" ]