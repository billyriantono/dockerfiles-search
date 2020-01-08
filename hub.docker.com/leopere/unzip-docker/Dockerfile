FROM alpine:latest
## The idea here is to just allow a single unzip function.  Compression isn't
## supported by Dockerfile ADD so we need something like this instead.

RUN apk update && apk add unzip

VOLUME /data
WORKDIR /data

## TODO: At some point maybe make this friendly for other people.
ENTRYPOINT ["unzip"]
