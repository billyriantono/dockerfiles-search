FROM alpine:latest

COPY entrypoint.sh /
RUN apk update; \
    apk upgrade; \
    apk add openssh; \
    apk add tmux; \
    \
    chmod +x /entrypoint.sh; \
    \
    # clean up
    rm -rf /var/cache/apk/* /tmp/*

RUN ssh-keygen -A

EXPOSE 22
ENTRYPOINT ["/entrypoint.sh"]
RUN date >/build-date.txt
