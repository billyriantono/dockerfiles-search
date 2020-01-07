FROM golang:1.12-stretch

RUN go get github.com/golang/mock/gomock \
    && go install github.com/golang/mock/mockgen \
    && go get github.com/google/wire/cmd/wire

RUN cd /go/src/github.com/golang/mock \
    && git checkout refs/tags/v1.2.0

