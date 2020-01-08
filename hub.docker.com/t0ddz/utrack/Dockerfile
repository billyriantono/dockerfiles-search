FROM golang:alpine as builder
ARG app_version
ENV VERSION=$app_version
ARG app_build
ENV BUILD=$app_build
RUN apk update && apk add --no-cache dep git ca-certificates tzdata && update-ca-certificates
COPY ./src/utrack $GOPATH/src/utrack
WORKDIR $GOPATH/src/utrack
RUN dep ensure
WORKDIR $GOPATH/src/utrack/cmd/utrackd
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-X main.Version=${VERSION} -X main.Build=${BUILD} -s -w" -a -installsuffix cgo -o /bin/utrackd .

FROM scratch
COPY --from=builder /usr/share/zoneinfo /usr/share/zoneinfo
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /bin/utrackd /bin/utrackd
COPY utrack.json /etc/utrack.json
VOLUME /data
ENTRYPOINT ["/bin/utrackd"]