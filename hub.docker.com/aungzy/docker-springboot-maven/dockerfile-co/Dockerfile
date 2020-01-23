FROM alpine:3.8 as builder

RUN apk --update --no-cache add \
        php7 \
        php7-json \
        php7-mbstring \
        php7-phar \
        php7-tokenizer \
    && wget https://cs.sensiolabs.org/download/php-cs-fixer-v2.phar \
        -O php-cs-fixer \
    && chmod a+x php-cs-fixer \
    && mv php-cs-fixer /usr/bin

FROM scratch

COPY --from=builder /bin /bin
COPY --from=builder /etc/php7 /etc/php7
COPY --from=builder [ \
    "/lib/ld-musl-x86_64.so.1", \
    "/lib/libc.musl-x86_64.so.1", \
    "/lib/libcrypto.so.43", \
    "/lib/libssl.so.45", \
    "/lib/libtls.so.17", \
    "/lib/libz.so.1", \
    "/lib/" \
]
COPY --from=builder /usr/bin /usr/bin
COPY --from=builder /usr/lib/php7 /usr/lib/php7
COPY --from=builder [ \
    "/usr/lib/libedit.so.0", \
    "/usr/lib/libncursesw.so.6", \
    "/usr/lib/libpcre.so.1", \
    "/usr/lib/libxml2.so.2", \
    "/usr/lib/" \
]

ENTRYPOINT ["/usr/bin/php-cs-fixer"]
