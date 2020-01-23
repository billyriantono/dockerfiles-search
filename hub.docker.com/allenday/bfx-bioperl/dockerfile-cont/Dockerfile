FROM        alpine:3.7 as incron-builder

ENV         VERSION=0.5.12

RUN         apk --no-cache add --virtual .build-deps \
                build-base \
                argp-standalone && \
            wget -q https://github.com/ar-/incron/archive/$VERSION.tar.gz -O - | tar xz && \
            ( \
                cd incron-$VERSION && \
                make -j$(nproc) && make install \
            ) && \
            apk del .build-deps

###

FROM        alpine:3.7 as s6-overlay-builder

ENV         VERSION=1.18.1.5

RUN         mkdir -p /rootfs && \
            wget -q https://github.com/just-containers/s6-overlay/releases/download/v$VERSION/s6-overlay-amd64.tar.gz -O - | tar xz -C /rootfs

###

FROM        allanlei/kubectl as kubectl

###

FROM        alpine:3.7
LABEL       maintainer="Allan Lei <allanlei@helveticode.com>"

ENTRYPOINT  ["/init"]
CMD         ["incrond", "--foreground"]

RUN         apk --no-cache add --virtual .run-deps \
                libstdc++ \
                bash

COPY        --from=s6-overlay-builder /rootfs/ /
COPY        --from=incron-builder /usr/local/sbin/ /usr/local/sbin/
COPY        --from=incron-builder /usr/local/bin/ /usr/local/bin/
COPY        --from=incron-builder /etc/incron.d/ /etc/incron.d/
COPY        --from=incron-builder /var/spool/incron/ /var/spool/incron/
COPY        --from=kubectl /usr/local/bin/ /usr/local/bin/
COPY        rootfs /
