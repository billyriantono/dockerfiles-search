FROM golang:1.10.3 AS builder

ENV VERSION 0.8.0
ENV CGO_ENABLED=0

WORKDIR /app
COPY . /app
RUN go get github.com/robfig/glock \
  && glock sync -n < GLOCKFILE

RUN go build -a -ldflags "-X main.buildVersion=$VERSION" -o docker-gen


FROM scratch

COPY --from=builder /app/docker-gen /

ENTRYPOINT [ "/docker-gen" ]
