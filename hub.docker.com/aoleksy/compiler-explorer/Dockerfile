FROM ubuntu:latest as fetcher
RUN true \
	&& apt update \
	&& apt upgrade --assume-yes \
	&& apt install --assume-yes --no-install-recommends \
		curl \
		gcc \
		git \
		gpg-agent \
		make \
		libc6-dev \
		software-properties-common \
	&& curl -sL https://deb.nodesource.com/setup_8.x | bash - \
	&& apt install --assume-yes --no-install-recommends \
		nodejs \
	&& git clone https://github.com/mattgodbolt/compiler-explorer.git \
	&& cd compiler-explorer \
	&& make prereqs

FROM ubuntu:latest
COPY --from=fetcher /compiler-explorer /compiler-explorer
COPY --from=fetcher /etc/apt /etc/apt
RUN \
	sed -i 's/https/http/' /etc/apt/sources.list.d/nodesource.list \
	&& apt update \
	&& apt install --assume-yes --no-install-recommends \
		git \
		g++ \
		make \
		nodejs \
	&& apt clean \
	&& rm -rf /var/lib/apt/lists/*
ENV EXTRA_ARGS="--host 0.0.0.0"
EXPOSE 10240
WORKDIR /compiler-explorer
CMD ["make"]
