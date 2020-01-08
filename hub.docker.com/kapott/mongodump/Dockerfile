FROM alpine:3.7
LABEL maintainer "Kapott <kapott+dockerfiles@aivd.33mail.com>"
RUN apk add --no-cache mongodb-tools
ENTRYPOINT ["mongodump"]
CMD ["--help"]
