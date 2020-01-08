FROM alpine

RUN apk --no-cache add git openssh

VOLUME /git
WORKDIR /git

ENTRYPOINT ["git"]
CMD ["--help"]