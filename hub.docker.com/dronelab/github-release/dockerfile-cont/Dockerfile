FROM alpine:3.3
MAINTAINER David Hallum <david@driveclutch.com>

RUN apk --update add \
		bash \
		curl \
		graphviz \
		ttf-dejavu \
	&& rm -rf \
		/var/cache/apk/* \
		/tmp/* \
	&& mkdir /graph \
	&& addgroup graph \
  && adduser -D -G graph -s /bin/bash -g "Graphviz Account" -h /graph graph

VOLUME /graph
WORKDIR /graph
CMD ["/bin/bash"]
