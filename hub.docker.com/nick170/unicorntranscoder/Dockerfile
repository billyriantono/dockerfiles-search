FROM frolvlad/alpine-glibc
LABEL maintainer="nicko170"

ENV UID=991 GID=991

ENV PORT=3000 \
	MOUNT_POINT="/media" \
	TRANSCODER_DECAY_TIME=120 \
	LOADBALANCER_ADDRESS="https://plex.devlan.io" \
	INSTANCE_ADDRESS="https://plex-transcoder.devlan.io" \
	REDIS_HOST="redis" \
	EAE_VERSION="eae-69c1de6-25" \
  CODECS_BUILD="392df4f-2183" \
  TRANSCODER_DEBUG="392df4f-2183"


COPY Transcoder/rootfs /


RUN apk add -U \
		npm \
		git \
		su-exec \
		s6 \
		binutils \
	&& mkdir -p /opt \
	&& cd /opt \
	&& git clone https://github.com/nicko170/UnicornTranscoder \
	&& cd UnicornTranscoder \
	&& npm install \
  && /opt/UnicornTranscoder/node_modules/.bin/grunt \
  && npm install \
	&& chmod a+x /usr/local/bin/* /etc/s6.d/*/* 

EXPOSE 3000

CMD ["run.sh"]
