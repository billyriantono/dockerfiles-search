FROM golang:1.13-alpine as build

WORKDIR /go/src/github.com/blakearoberts/k8s-job-runner

ADD . /go/src/github.com/blakearoberts/k8s-job-runner

RUN go mod download && \
    go build -o k8s-job-runner && \
    go install

FROM alpine

USER nobody

COPY --from=build /go/bin/k8s-job-runner $HOME/bin/

ENTRYPOINT [ "k8s-job-runner" ]
