FROM runmymind/docker-android-sdk:ubuntu-standalone

RUN apt-get update -qq
RUN apt-get update && apt-get install -y --no-install-recommends \
	libc6 \
	libstdc++6 \
	libgcc1 \
	libncurses5 \
	libz1 \
	locales \
	python2.7 \
	python2.7-dev \
	libssl-dev \
	ssh \
	wget \
	rsync \
	curl \
	git-all \
	unzip \
	&& rm -rf /var/lib/apt/lists/*

RUN ln -s /usr/bin/python2.7 /usr/bin/python
RUN locale-gen en_US.UTF-8
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

# Cleaning
RUN apt-get clean
