FROM alpine:latest

LABEL maintainer="tantan0"

RUN apk add --no-cache git

VOLUME /git
WORKDIR /git

ENTRYPOINT ["git"]
CMD ["--help"]
