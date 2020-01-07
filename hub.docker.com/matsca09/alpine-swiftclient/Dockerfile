FROM alpine:3.7 AS builder

RUN apk update && apk add python2 python2-dev py2-pip alpine-sdk linux-headers && \
	pip install --user python-keystoneclient python-swiftclient


FROM alpine:3.7 
COPY --from=builder /root/.local /usr/
RUN apk update && apk add python2 py2-pip && rm -rf /var/cache/apk
