FROM alpine

RUN apk --no-cache add git openssh

VOLUME /app
WORKDIR /app

ENTRYPOINT ["git"]
CMD ["--help"]
