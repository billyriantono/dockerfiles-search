FROM alpine:3.10

ARG PANDOC_VERSION="${PANDOC_VERSION:-2.7.3}"

RUN wget https://github.com/jgm/pandoc/releases/download/"$PANDOC_VERSION"/pandoc-"$PANDOC_VERSION"-linux.tar.gz \
    &&  tar -xzvf pandoc-"$PANDOC_VERSION"-linux.tar.gz \
    && mv pandoc-"$PANDOC_VERSION"/bin/pandoc /usr/local/bin \
    && rm -rf pandoc-"$PANDOC_VERSION" pandoc-"$PANDOC_VERSION"-linux.tar.gz \
    && apk add --no-cache texlive


WORKDIR /data

ENTRYPOINT ["pandoc"]

CMD ["--help"]
