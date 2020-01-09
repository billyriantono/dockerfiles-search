# reference https://hub.docker.com/_/golang/
# reference https://docs.docker.com/engine/reference/builder/

FROM golang:alpine
MAINTAINER MiddleCoast LLC <info@middlecoast.io>

RUN apk update && apk upgrade && \
apk add --no-cache bash git

ARG ARG_REPO
ARG ARG_BRANCH

ENV REPO=${ARG_REPO}
ENV BRANCH=${ARG_BRANCH}
ENV GOBIN="/go/src/app"

RUN mkdir -p /go/src/app
RUN git clone --depth=1 --branch=${BRANCH} ${REPO} /go/src/app

WORKDIR /go/src/app
RUN go build -v -o ssoapi cmd/ssoapi.endpoint.go

EXPOSE 8080/tcp

CMD ["./ssoapi"]