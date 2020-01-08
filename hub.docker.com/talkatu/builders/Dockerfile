FROM talkatu/builders:debian-buster-amd64

MAINTAINER Gary Kramlich <grim@reaperworld.com>

RUN set -ex && \
	apt-get update && \
	apt-get install -y --no-install-recommends clang-tools && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists

COPY scanbuild/scan-build /usr/local/bin

COPY scanbuild/build.sh /

