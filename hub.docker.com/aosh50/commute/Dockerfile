FROM golang:1.11.1-alpine3.8 as build-env

RUN sed -i -e 's/v[[:digit:]]\.[[:digit:]]/edge/g' /etc/apk/repositories
RUN apk update
RUN apk add alpine-sdk

RUN go version

RUN mkdir -p commute
WORKDIR /commute

COPY go.mod .
RUN go get

ADD . .

RUN go build

FROM alpine:3.8
RUN apk update

WORKDIR /app
COPY --from=build-env /commute/commute .
RUN ls
RUN mkdir -p config
EXPOSE 3333
CMD ["./commute"]