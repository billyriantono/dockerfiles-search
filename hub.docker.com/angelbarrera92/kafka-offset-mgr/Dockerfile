FROM debian:stretch as builder
RUN apt-get update && \
    apt-get install -y curl ca-certificates zip && \
    curl -O -L -s https://github.com/serejja/kafka-offset-mgr/releases/download/v0.1.0/kafka-offset-mgr_linux_amd64.zip && \
    unzip kafka-offset-mgr_linux_amd64.zip && \
    chmod +x /kafka-offset-mgr

FROM debian:stretch
COPY --from=builder /kafka-offset-mgr /
ENTRYPOINT /kafka-offset-mgr
