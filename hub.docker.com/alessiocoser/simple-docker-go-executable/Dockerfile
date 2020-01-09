FROM golang:1.9-alpine
COPY entrypoint.sh /
WORKDIR /go/src/app
ENTRYPOINT ["/entrypoint.sh"]
CMD ["version"]