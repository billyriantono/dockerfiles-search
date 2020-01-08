FROM phusion/baseimage:0.9.17

ENV RUBY_MAJOR 2.3
ENV RUBY_VERSION 2.3.0
ENV RUBY_DOWNLOAD_SHA256 ba5ba60e5f1aa21b4ef8e9bf35b9ddb57286cb546aac4b5a28c71f459467e507
ENV RUBYGEMS_VERSION 2.5.2

# skip installing gem documentation
RUN echo 'install: --no-document\nupdate: --no-document' >> "$HOME/.gemrc"

# some of ruby's build scripts are written in ruby
# we purge this later to make sure our final image uses what we just built
RUN \
  apt-get update && \
  apt-get install -y autoconf bison git-core libgdbm-dev build-essential libssl-dev libreadline-gplv2-dev libxml2-dev libxslt1-dev libpq-dev libmysqlclient-dev libsqlite3-dev ruby libgmp3-dev &&\
	rm -rf /var/lib/apt/lists/* && \
	mkdir -p /usr/src/ruby && \
	curl -fSL -o ruby.tar.gz "http://cache.ruby-lang.org/pub/ruby/$RUBY_MAJOR/ruby-$RUBY_VERSION.tar.gz" && \
	echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.gz" | sha256sum -c - && \
	tar -xzf ruby.tar.gz -C /usr/src/ruby --strip-components=1 && \
	rm ruby.tar.gz && \
	cd /usr/src/ruby && \
	autoconf && \
	./configure --disable-install-doc && \
	make -j"$(nproc)" && \
	make install && \
	apt-get purge -y --auto-remove bison libgdbm-dev ruby && \
	gem update --system $RUBYGEMS_VERSION && \
	rm -r /usr/src/ruby && \
	export LC_ALL=C.UTF-8 && \
	export LANG=en_US.UTF-8 && \
	export LANGUAGE=en_US.UTF-8

# install things globally, for great justice
ENV GEM_HOME /usr/local/bundle
ENV PATH $GEM_HOME/bin:$PATH

ENV BUNDLER_VERSION 1.11.2

RUN gem install bundler --version "$BUNDLER_VERSION" && \
	bundle config --global path "$GEM_HOME" && \
	bundle config --global bin "$GEM_HOME/bin" && \
	bundle config --global silence_root_warning true
