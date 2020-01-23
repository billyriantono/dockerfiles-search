FROM golang:alpine AS builder

LABEL maintainer="Aivars Sterns <atoms@tups.lv>"

RUN apk update && apk add --no-cache git

WORKDIR $GOPATH/src/github.com/latency_exporter/
COPY . .
RUN go get -d -v
RUN go build -o /go/bin/latency_exporter


#### 
FROM scratch
COPY --from=builder /go/bin/latency_exporter /go/bin/latency_exporter
ENTRYPOINT ["/go/bin/latency_exporter"]