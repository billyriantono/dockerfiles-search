FROM golang:1.12
WORKDIR $GOPATH/src/github.com/autenti-devops/ajb
COPY . .
RUN CGO_ENABLED=0 GOOS=linux make

FROM alpine:latest
WORKDIR /root/
COPY --from=0 /go/src/github.com/autenti-devops/ajb/output/ajb .
COPY ./examples/configs/ .
EXPOSE 9090
CMD ./ajb