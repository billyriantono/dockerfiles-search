FROM golang:1.8.4-jessie


RUN cd /tmp \
    && apt-get update \
    && apt-get install -y \
        git

RUN go get github.com/ugorji/go/codec \
	&& go get gopkg.in/alexcesaro/statsd.v2 \
	&& go get gopkg.in/redis.v5
