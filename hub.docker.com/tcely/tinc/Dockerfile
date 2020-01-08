FROM alpine:edge
LABEL maintainer="https://keybase.io/tcely"

RUN apk --update upgrade && \
    apk add ca-certificates less man tinc tinc-doc bash && \
    rm -rf /var/cache/apk/*

EXPOSE 655/tcp 655/udp
VOLUME /etc/tinc

ENV PAGER=less
ENTRYPOINT ["/usr/sbin/tincd", "-D"]
CMD ["-d"]
