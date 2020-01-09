FROM alpine:3.10

RUN apk --update add git less openssh bash && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

VOLUME /git
WORKDIR /git

ENTRYPOINT ["/bin/bash", "-c"]
CMD ["git", "--help"]