FROM alpine:3.7

RUN \
  echo "⦿ Updating APK" && \
    apk update && \
  echo "⦿ Installing certbot" && \
    apk add certbot && \
  echo "⦿ Cleaning up" && \
    rm -f /var/cache/apk/*

EXPOSE 80 443
WORKDIR /root
