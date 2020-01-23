# Latest nightly floss build
# Until I figure out a slim, glibc version of alpine to support Floss
#
# 6 layers, ~89 MB
#
FROM debian:buster-slim

LABEL maintainer="Thomas"

RUN apt update && apt install -y \
	ca-certificates \
	wget \
	--no-install-recommends \
	&& wget -O /usr/local/bin/floss https://s3.amazonaws.com/build-artifacts.floss.flare.fireeye.com/travis/linux/dist/floss \
	&& chmod +x /usr/local/bin/floss \
	&& mkdir /tester \
	&& rm -rf /var/lib/apt/lists/*

WORKDIR /tester

ENTRYPOINT [ "floss" ]

CMD [ "-h" ]
