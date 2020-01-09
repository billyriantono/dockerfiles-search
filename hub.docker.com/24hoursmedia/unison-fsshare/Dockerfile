FROM alpine:latest

RUN apk --no-cache add unison

RUN mkdir -p /mnt/master
RUN mkdir -p /mnt/replica

VOLUME /mnt/master
VOLUME /mnt/replica

COPY default.prf /root/.unison/default.prf
COPY run-unison.sh /run-unison.sh
RUN chmod +x /run-unison.sh

ENTRYPOINT ["/run-unison.sh"]