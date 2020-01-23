FROM alpine

ENTRYPOINT ["/entrypoint.sh"]
ADD /entrypoint.sh /entrypoint.sh
RUN chmod 755 /entrypoint.sh

ENV \
    TERM=xterm \
    AUTOSSH_LOGFILE=/dev/stdout \
    AUTOSSH_GATETIME=30         \
    AUTOSSH_POLL=10             \
    AUTOSSH_FIRST_POLL=30       \
    AUTOSSH_LOGLEVEL=1

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community/" >> /etc/apk/repositories && \
    apk update && \
    apk add --update autossh && \
    rm -rf /var/lib/apt/lists/*
