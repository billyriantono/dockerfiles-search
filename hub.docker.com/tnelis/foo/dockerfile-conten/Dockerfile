FROM tim03/curl
MAINTAINER Chen, Wenli <chenwenli@chenwenli.com>
RUN apt-get -qq update && apt-get install -qqy --no-install-recommends \
		git \
		mercurial \
		openssh-client \
		subversion \
        && apt-get -y autoremove \
        && apt-get clean \
	&& rm -rf /var/lib/apt/lists/*
