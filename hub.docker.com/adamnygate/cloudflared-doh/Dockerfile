FROM alpine:latest

WORKDIR /usr/local/bin
ENV LOCAL_PORT	53
ENV CLOUDFLARED=cloudflared

RUN apk update && \
    apk upgrade && \
    apk add libc6-compat && \
    apk add ca-certificates

EXPOSE $LOCAL_PORT/tcp	$LOCAL_PORT/udp

ADD https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.tgz $CLOUDFLARED.tgz
RUN tar -xvzf $CLOUDFLARED.tgz
RUN rm $CLOUDFLARED.tgz

RUN chmod u+x $CLOUDFLARED
RUN $CLOUDFLARED update
ENTRYPOINT $CLOUDFLARED proxy-dns --port $LOCAL_PORT --address 0.0.0.0
