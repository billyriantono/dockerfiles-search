#
# ----- Go Builder Image ------
#
FROM golang:1.12-alpine AS builder

RUN apk add --no-cache git bats

# set working directory
RUN mkdir -p /go/src/app
WORKDIR /go/src/app

# copy sources
COPY . .

# build
RUN CGO_ENABLED=0 GO111MODULE=on go build -o /bin/kubetest

# test
RUN kubetest --help
RUN ./acceptance.bats

#
# ------ Kubetest runtime image ------
#
FROM scratch

# this is the last commabd since it's never cached
COPY --from=builder /bin/kubetest /kubetest

ENTRYPOINT ["/kubetest"]
CMD ["--help"]
