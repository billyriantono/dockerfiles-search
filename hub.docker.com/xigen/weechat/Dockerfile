FROM alpine

MAINTAINER Chris Hilsdon <chris@xigen.io>

ENV LANG C.UTF-8
ENV HOME /weechat

RUN apk add --update \
    weechat-aspell \
    weechat-python \
    weechat-perl \
    weechat-lua \
    python \
    py-pip \
    bash \
    && rm -rf /var/cache/apk/*

RUN mkdir -p $HOME/.weechat \
    && addgroup weechat \
    && adduser -h $HOME -D -s /bin/bash -G weechat weechat \
    && chown -R weechat:weechat $HOME \
    && pip install websocket-client

COPY entrypoint.sh /entrypoint.sh

RUN chmod a+x /entrypoint.sh

VOLUME /weechat/.weechat

WORKDIR $HOME

USER weechat

ENTRYPOINT ["/entrypoint.sh"]
