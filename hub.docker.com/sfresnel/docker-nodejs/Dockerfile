FROM debian:jessie

RUN apt-get update -y && \
	apt-get install --no-install-recommends -y -q \
		curl \
		python \
		build-essential \
		git \
		ca-certificates && \
	apt-get clean && \
	mkdir /nodejs && \
	curl https://nodejs.org/dist/latest-v0.12.x/node-v0.12.17-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1

ENV PATH $PATH:/nodejs/bin