#  The following is the "build" phase 
FROM golang:1.11.10-alpine3.9 as BUILD

ENV PROJECT_PATH /go/src/github.com/7onetella/tester
WORKDIR $PROJECT_PATH
ADD . $PROJECT_PATH
RUN set -xe \
   && go build -o tester

#  The following is the "ship" phase 
FROM alpine:3.9

COPY --from=BUILD /go/src/github.com/7onetella/tester/tester /
COPY --from=BUILD /go/src/github.com/7onetella/tester/morgan /
COPY --from=BUILD /go/src/github.com/7onetella/tester/entrypoint.sh /
RUN chmod +x /tester \
    && chmod +x /morgan \
    && chmod +x /entrypoint.sh \
    && apk add --no-cache ca-certificates
EXPOSE 8080

# https://medium.com/@gchudnov/trapping-signals-in-docker-containers-7a57fdda7d86
# make sure to call exec form to be able to receive SIGTERM for deregistering from Consul
ENTRYPOINT ["/tester"]