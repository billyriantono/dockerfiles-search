FROM debian:9.9

RUN \
    apt-get update && \
    apt-get install -y curl unzip && \
    curl https://rclone.org/install.sh | bash && \
    apt-get purge -y curl unzip

ENTRYPOINT [ "rclone" ]
