FROM golang AS build

ARG ARCH
COPY README.md qemu-${ARCH}-static* /usr/bin

MAINTAINER Neszt Tibor <tibor@neszt.hu>

RUN \
	go get -d github.com/lomik/go-carbon && \
	cd /go/src/github.com/lomik/go-carbon && \
	sed -i 's/math.MaxInt64/maxInt/g' vendor/github.com/go-graphite/go-whisper/compress.go && \
	sed -i "/^\t\"sort/a\\\t\"strconv\"" vendor/github.com/go-graphite/go-whisper/compress.go && \
	sed -i "/^const.sizeEstimationBuffer/a\\const maxInt = 1<<uint(strconv.IntSize-1) - 1" vendor/github.com/go-graphite/go-whisper/compress.go && \
	CGO_ENABLED=0 go get github.com/lomik/go-carbon && \
	strip /go/bin/go-carbon

FROM scratch

COPY --from=build /go/bin/go-carbon /

WORKDIR /data

CMD ["/go-carbon", "-config", "/data/carbon.conf"]
