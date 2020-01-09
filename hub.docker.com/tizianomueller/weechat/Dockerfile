FROM alpine:edge

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="e.g. https://github.com/dev-zero/docker-images"

RUN apk add --no-cache --update \
    bash \
    shadow \
    coreutils \
    tmux \
    tzdata \
    weechat \
    weechat-aspell \
    weechat-ruby \
    weechat-lua \
    weechat-perl \
    weechat-python

ENV \
    TERM=screen-256color \
    PUID=1000 \
    PGID=1000

ENV \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8 \
    LC_TIME=de_CH.utf8 \
    LC_MONETARY=de_CH.utf8 \
    LC_NUMERIC=de_CH.utf8 \
    TZ=Europe/Zurich

RUN groupadd -g ${PGID} weechat
RUN useradd -g ${PGID} -u ${PUID} -m -s /bin/bash -d /weechat weechat

RUN ln -snf /usr/share/zoneinfo/"${TZ}" /etc/localtime && echo "${TZ}" > /etc/timezone

COPY start.sh /start.sh

EXPOSE 9001

USER weechat

COPY tmux.conf /weechat/.tmux.conf
HEALTHCHECK CMD tmux has-session -t weechat
CMD /start.sh
WORKDIR /weechat
VOLUME /weechat
