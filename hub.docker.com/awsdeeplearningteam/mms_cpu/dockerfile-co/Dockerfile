FROM debian:jessie
RUN apt-get update \
	&& apt-get install --no-install-recommends --no-install-suggests -y stress \
	&& rm -rf /var/lib/apt/lists/*
ENTRYPOINT ["stress"]