FROM hyperized/scratch:latest as trigger
# Used to trigger Docker hubs auto build, which it wont do on the official images

FROM golang:alpine as builder

RUN apk -U add git build-base libsass-dev
RUN git clone https://github.com/gohugoio/hugo.git
WORKDIR hugo
RUN go install --tags extended

FROM alpine:latest

LABEL maintainer="Gerben Geijteman <gerben@hyperized.net>"
LABEL description="Hugo in Docker"

RUN apk -U add libsass
COPY --from=builder /go/bin/hugo /hugo
WORKDIR /project
ENTRYPOINT ["/hugo"]
CMD ["--help"]
