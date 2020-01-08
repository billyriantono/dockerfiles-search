FROM ubuntu:14.04

RUN apt-get update && \
	apt-get install -y build-essential vim python procps numactl curl git zlib1g-dev libffi-dev libssl-dev libreadline-dev libyaml-dev libxml2-dev lsof libxslt-dev && \
	curl -sL https://deb.nodesource.com/setup | bash - && \
	apt-get install -y nodejs && \
	npm install -g coffee-script && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*
