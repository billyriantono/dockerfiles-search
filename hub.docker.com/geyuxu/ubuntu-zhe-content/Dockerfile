FROM erlio/docker-vernemq:1.6.0

ENV DOCKER_VERNEMQ_ALLOW_ANONYMOUS=on \
    DOCKER_VERNEMQ_RETRY_INTERVAL=1 \
    DOCKER_VERNEMQ_LOG__CONSOLE__LEVEL=debug

EXPOSE 1883:1883

CMD ["start_vernemq"]