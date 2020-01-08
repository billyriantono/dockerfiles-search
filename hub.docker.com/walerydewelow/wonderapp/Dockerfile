FROM golang:1.12.9-alpine AS build

COPY . /go/src/wonderapp
RUN go install wonderapp

FROM alpine:3

COPY --from=build /go/bin/wonderapp /

ENTRYPOINT [ "/wonderapp" ]
