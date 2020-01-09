FROM alpine:3.8

LABEL maintainer="arg0t"

RUN apk add py2-pip python2-dev ffmpeg && \
    pip --no-cache-dir install requests requests[security] requests-cache babelfish "guessit<2" "subliminal<2" && \
    pip uninstall -y stevedore && \
    pip --no-cache-dir install stevedore==1.19.1 python-dateutil qtfaststart
