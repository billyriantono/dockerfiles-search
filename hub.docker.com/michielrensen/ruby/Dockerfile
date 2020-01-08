FROM chef/chefdk:1.2.22

ENV BUNDLER_VERSION 1.15.1

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		build-essential \
		make \
	&& rm -rf /var/lib/apt/lists/*

RUN gem update --system \
 && gem install bundler --version "$BUNDLER_VERSION"
