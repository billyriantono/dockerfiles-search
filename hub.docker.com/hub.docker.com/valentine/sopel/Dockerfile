# Copyright 2018 Valentine C

FROM woahbase/alpine-s6

MAINTAINER Valentine C

RUN apk add --update \
    python3 \
    ca-certificates \
    enchant \
    && pip3 install \
    sopel \
    ipython \
    && rm -rf /tmp/* /var/cache/apk/*

VOLUME ["/sopel"]

COPY 01-sopel etc/fix-attrs.d/01-sopel
COPY sopel-run.sh etc/services.d/sopel/run

ENTRYPOINT ["/init"]
