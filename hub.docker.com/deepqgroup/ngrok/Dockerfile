FROM golang:1.11.5 as compiler
WORKDIR /go
COPY . .
RUN make release-server
ENTRYPOINT /go/bin/ngrokd