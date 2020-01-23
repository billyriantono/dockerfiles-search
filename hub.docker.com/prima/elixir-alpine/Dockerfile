FROM bitwalker/alpine-elixir:1.5.0

RUN apk --update add unzip \
                     ncurses-libs \
                     groff \
                     less \
                     python \
                     py-pip \
                     curl \
                     tar \
                     gzip \
                     vim \
                     tzdata && \
                     pip install awscli && \
                     apk --purge del py-pip unzip wget tzdata && \
                     rm -rf /var/cache/apk/*

COPY files/setup_common.sh /setup_common.sh

ENTRYPOINT ["/bin/sh"]
