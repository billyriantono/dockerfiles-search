FROM alpine:3.9

LABEL maintainer='leifcr@gmail.com'
LABEL description='Alpine with jq and curl'

LABEL maintainer Leif Ringstad <leifcr@gmail.com>

RUN apk add --update --no-cache \
	dumb-init bash openssl jq curl \
	&& rm -fr /var/cache/apk/*

CMD ["/bin/bash"]
