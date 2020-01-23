# Dockerfile for Tribe GoBGP Image
FROM golang@sha256:8dea7186cf96e6072c23bcbac842d140fe0186758bcc215acb1745f584984857 as builder

RUN apk update && apk add --no-cache git gcc linux-headers musl-dev

USER root
WORKDIR /root

# Fetch dependencies.

# Using go get.
RUN go get -u github.com/golang/dep/cmd/dep \
    && go get -d github.com/osrg/gobgp \
    # Since there are no go files in the root it comes back as error. || prevents this.
    || cd ${GOPATH}/src/github.com/osrg/gobgp \
    && dep ensure -v \
    && CGO_ENABLED=0 GOOS=linux go build -ldflags="-w -s" -a -installsuffix cgo -o /go/bin/gobgp ./cmd/gobgp \
    && CGO_ENABLED=0 GOOS=linux go build -ldflags="-w -s" -a -installsuffix cgo -o /go/bin/gobgpd ./cmd/gobgpd


FROM scratch

# Copy our static executable
COPY --from=builder /go/bin/gobgp /go/bin/gobgp
COPY --from=builder /go/bin/gobgpd /go/bin/gobgpd
WORKDIR /gobgp

# Run the gobgpd binary.
ENTRYPOINT ["/go/bin/gobgpd"]
