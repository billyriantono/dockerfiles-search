FROM alpine
LABEL maintainer="Anatoly Milkov <mail@amilkov.net>"

ADD entrypoint.sh /entrypoint.sh
RUN apk add --no-cache dumb-init beanstalkd && \
    chmod +x /entrypoint.sh

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

CMD ["/entrypoint.sh"]

EXPOSE 11300

VOLUME ["/data"]
