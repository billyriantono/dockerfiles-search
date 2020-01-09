FROM alpine:3.4

RUN apk update && \
  apk add \
    ca-certificates \
    openssh-client bash && \
  rm -rf /var/cache/apk/*

ADD run.sh /bin/
CMD ["/bin/run.sh"]