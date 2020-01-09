FROM alpine:latest

RUN apk --no-cache add unzip hugo curl ca-certificates && \
    curl -s https://downloads.rclone.org/rclone-current-linux-amd64.zip > /tmp/rclone.zip && \
    unzip -qc /tmp/rclone.zip *rclone > /usr/local/bin/rclone && \
    chmod +x /usr/local/bin/rclone && \
    rm -f /tmp/rclone.zip && apk --no-cache del unzip curl 

ENTRYPOINT ["/bin/sh"]
