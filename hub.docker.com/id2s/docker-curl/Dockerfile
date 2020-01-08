FROM debian:jessie

RUN apt-get update \
	&& apt-get install -y ca-certificates curl --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

CMD ["bash"]