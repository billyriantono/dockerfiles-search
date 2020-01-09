#### Build Container ####
FROM alpine as builder

WORKDIR /tmp
COPY ./build-rclone.sh /tmp/build-rclone.sh

RUN apk --no-cache add unzip wget

RUN /bin/sh /tmp/build-rclone.sh

RUN unzip rclone.zip
RUN cd rclone-*-linux-* \
    && cp rclone /usr/bin/
RUN chown root:root /usr/bin/rclone
RUN chmod 755 /usr/bin/rclone


#### Runtime Container ####
FROM alpine

COPY --from=builder /usr/bin/rclone /usr/bin/rclone
RUN apk --no-cache add ca-certificates

ENTRYPOINT ["/usr/bin/rclone"]
