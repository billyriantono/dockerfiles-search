FROM alpine:3.10


RUN apk add --no-cache tini && \
    wget -O /usr/bin/wait-for https://raw.githubusercontent.com/eficode/wait-for/master/wait-for && \
    chmod +x /usr/bin/wait-for

ENTRYPOINT [ "tini", "--", "wait-for"]
