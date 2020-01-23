FROM prima/rust:1.40.0

# node
RUN apt-get update && \
    apt-get install -qqy openssh-client \
    jq \
    git && \
    apt-get clean

COPY files/entrypoint.sh /entrypoint

CMD ["./entrypoint"]
