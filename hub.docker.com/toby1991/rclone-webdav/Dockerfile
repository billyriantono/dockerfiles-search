############################
# STEP 1 build executable binary
############################
FROM alpine:latest AS builder
ENV RCLONE_VERSION=v1.48.0
WORKDIR /bin/
RUN wget https://github.com/ncw/rclone/releases/download/${RCLONE_VERSION}/rclone-${RCLONE_VERSION}-linux-amd64.zip -O ./rclone.zip \ 
	&& unzip ./rclone.zip -d ./ \ 
	&& mv ./rclone-${RCLONE_VERSION}-linux-amd64/rclone ./rclone

############################
# STEP 2 build a small server image
############################
FROM alpine:latest
ENV BUCKET=rclone
ENV AUTH_USER=rclone
ENV AUTH_PASS=rclone123

COPY ./rclone.conf /root/.config/rclone/rclone.conf
COPY --from=builder /bin/rclone /rclone
WORKDIR /

# Run the server binary.
ENTRYPOINT /rclone -v --no-check-certificate serve webdav minio:${BUCKET} --disable-dir-list --vfs-cache-mode writes --addr :80 --user ${AUTH_USER} --pass ${AUTH_PASS} 
EXPOSE 80
