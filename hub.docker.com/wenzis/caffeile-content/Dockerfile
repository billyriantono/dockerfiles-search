FROM ruby:2.1
LABEL maintainer "YipYip <devops@yipyip.nl>"

ENV ELIXIR_VERSION="v1.7.3"
ENV ELIXIR_DOWNLOAD_SHA256="c9beabd05e820ee83a56610cf2af3f34acf3b445c8fabdbe98894c886d2aa28e"
ENV LANG=C.UTF-8

RUN wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && dpkg -i erlang-solutions_1.0_all.deb
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get update && apt-get install -y nodejs build-essential inotify-tools esl-erlang curl ca-certificates unzip && npm install npm -g
RUN npm install -g \
	brunch \
	node-gyp

RUN set -xe \
	&& ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/${ELIXIR_VERSION}.tar.gz" \
	&& ELIXIR_DOWNLOAD_SHA256="${ELIXIR_DOWNLOAD_SHA256}" \
	&& curl -fSL -o elixir-src.tar.gz $ELIXIR_DOWNLOAD_URL \
	&& echo "$ELIXIR_DOWNLOAD_SHA256  elixir-src.tar.gz" | sha256sum -c - \
	&& mkdir -p /usr/local/src/elixir \
	&& tar -xzC /usr/local/src/elixir --strip-components=1 -f elixir-src.tar.gz \
	&& rm elixir-src.tar.gz \
	&& cd /usr/local/src/elixir \
	&& make install clean

RUN gem install sass -v 3.6.0
RUN gem install compass

CMD ["iex"]