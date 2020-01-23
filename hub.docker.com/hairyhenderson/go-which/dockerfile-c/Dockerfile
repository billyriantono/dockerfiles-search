ARG GO_VERSION=1.13.0

FROM hahaman/docker-gobase AS builder

ENV APP_DIR=$GOPATH/src/restkaf/
RUN mkdir -p $APP_DIR

ADD . $APP_DIR
WORKDIR $APP_DIR

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go install restkaf

#####################################################################3
# final stage
FROM alpine:latest
RUN apk --no-cache add ca-certificates
COPY --from=builder /go/bin/restkaf ./
COPY --from=builder /go/src/restkaf/config.yml ./

RUN chmod +x ./restkaf
ENTRYPOINT ["./restkaf"]
EXPOSE 8080