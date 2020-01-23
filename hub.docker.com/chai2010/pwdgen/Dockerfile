FROM golang:alpine as builder
RUN apk add --update git && go get github.com/chai2010/pwdgen

FROM alpine
COPY --from=builder /go/bin/pwdgen /usr/bin/

ENTRYPOINT ["/usr/bin/pwdgen"]
CMD ["-h"]
