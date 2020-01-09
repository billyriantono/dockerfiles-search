# build go program first
FROM golang as builder

WORKDIR $GOPATH/src/github.com/qinhan-shu/dep-demo/

ADD ./. .

ENV CGO_ENABLED=0

RUN ls
RUN go build -o dep-demo ./main.go

RUN cp dep-demo /usr/local/bin/


FROM alpine:latest

WORKDIR /usr/local/bin

# Put go executeable to bin
COPY --from=builder /usr/local/bin/dep-demo .

EXPOSE 12345

CMD ["/usr/local/bin/dep-demo"]
