FROM golang:1.10

RUN go get -u golang.org/x/vgo \
  && cd /go/src/golang.org/x/vgo \
  && git checkout 3579ffcf11c94d03d3f236a7bbe3d1e4533bacd2 \
  && go install
