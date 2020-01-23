FROM golang:1.12.6 AS build_stage

WORKDIR /srv

COPY . /srv

ENV GOOS=linux
ENV GOARCH=amd64
ENV CGO_ENABLED=0
ENV GO111MODULE=on

RUN go build -o /srv/bin/fake-rabbitmq-consumer cmd/main.go

FROM alpine:3.9.4 AS prod_stage

COPY --from=build_stage /srv/bin/fake-rabbitmq-consumer /bin/fake-rabbitmq-consumer
RUN apk --no-cache add ca-certificates

ENTRYPOINT ["/bin/fake-rabbitmq-consumer"]
