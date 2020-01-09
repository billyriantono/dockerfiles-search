FROM alpine:latest

RUN apk update && \
    apk add \
        bash \
        conntrack-tools \
        libmnl \
        libnfnetlink

ENTRYPOINT ["conntrack"]
CMD []
