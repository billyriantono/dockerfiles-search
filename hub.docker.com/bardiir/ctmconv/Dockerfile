FROM ubuntu:16.04

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		openctm-tools \
	&& apt-get -y autoremove \
	&& rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["ctmconv"]
