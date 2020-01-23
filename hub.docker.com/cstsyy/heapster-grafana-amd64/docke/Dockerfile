FROM alpine:3.6
COPY nic-info.sh /root/nic-info.sh
RUN apk update && \
    apk add bash ethtool grep
ENTRYPOINT ["/root/nic-info.sh"]

