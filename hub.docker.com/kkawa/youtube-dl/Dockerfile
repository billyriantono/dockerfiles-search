FROM alpine

RUN apk add --no-cache ca-certificates \
                       ffmpeg \
                       openssl \
                       python3 \
    && pip3 install youtube-dl

WORKDIR /data
VOLUME ["/data"]

ENTRYPOINT ["youtube-dl"]
CMD ["--help"]
