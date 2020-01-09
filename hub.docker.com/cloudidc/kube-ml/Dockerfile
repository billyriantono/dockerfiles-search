FROM golang:alpine as builder
RUN apk add git
COPY . /workspace
WORKDIR /workspace
ARG GO_PACKAGE=github.com/cloudidc/kube-ml
RUN go build -ldflags "\
  -X ${GO_PACKAGE}/pkg/version.gitVersion=$(git rev-parse --abbrev-ref HEAD) \
  -X ${GO_PACKAGE}/pkg/version.gitCommit=$(git rev-parse HEAD) \
  -X ${GO_PACKAGE}/pkg/version.buildDate=$(date -u +'%Y-%m-%dT%H:%M:%SZ')" \
  -o /workspace/bin/kube-ml \
  ${GO_PACKAGE}/cmd/kube-ml

FROM alpine:3.10
COPY --from=builder /workspace/bin/kube-ml /bin/kube-ml
CMD ["/bin/kube-ml"]