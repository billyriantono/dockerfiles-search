FROM alpine:3.6


RUN : \
 && apk update && apk upgrade \
 && apk add --no-cache \
    openssh-client \
    rsync \
 && rm -rf /var/cache/apk/* \
 && :


COPY docker-entrypoint.sh /


ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["sh"]
