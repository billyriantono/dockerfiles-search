FROM exelban/baseimage:golang-latest as build

WORKDIR /app/
COPY . /app/
ENV GO111MODULE=on
RUN go build -mod vendor -o ./bin/main


FROM exelban/baseimage:alpine-latest

MAINTAINER Serhiy Mitrovtsiy <mitrovtsiy@ukr.net>
COPY --from=build /app/bin /
ENTRYPOINT ./main