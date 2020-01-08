
# @see https://github.com/docker-library/ruby/blob/master/2.3/stretch/slim/Dockerfile
# @see https://bugs.ruby-lang.org/issues/6383#note-1
# @see https://gist.github.com/mislav/055441129184a1512bb5

FROM debian:stretch-slim

ENV RUBY_MAJOR 1.8
ENV RUBY_VERSION 1.8.7-p358
ENV RUBYGEMS_VERSION 1.8.30

ADD no-sslv3-patch.diff /
RUN set -ex \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends \
		bzip2 \
		ca-certificates \
		libffi-dev \
		libgdbm3 \
		libssl1.0-dev \
		libyaml-dev \
		procps \
		zlib1g-dev \
	&& savedAptMark="$(apt-mark showmanual)" \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends \
		autoconf \
		bison \
		dpkg-dev \
		gcc \
		libbz2-dev \
		libgdbm-dev \
		libglib2.0-dev \
		libgmp-dev \
		libncurses-dev \
		libreadline-dev \
		libxml2-dev \
		libxslt-dev \
		make \
		wget \
		xz-utils \
	&& rm -rf /var/lib/apt/lists/* \
	&& wget -O /ruby.tar.gz "https://cache.ruby-lang.org/pub/ruby/ruby-$RUBY_VERSION.tar.gz" \
	&& mkdir -p /usr/local/src/ruby \
	&& tar -zxf /ruby.tar.gz -C /usr/local/src/ruby --strip-components=1 \
	&& rm /ruby.tar.gz \
	&& cd /usr/local/src/ruby \
	&& patch -p1 < /no-sslv3-patch.diff \
	&& rm /no-sslv3-patch.diff \
	&& CFLAGS="-O2 -fno-tree-dce -fno-optimize-sibling-calls" ./configure \
	&& make -j $(nproc) \
	&& make install \
	&& cd / \
	&& rm -rf /usr/local/src/ruby \
	&& wget -O /rubygems.tgz "https://github.com/rubygems/rubygems/releases/download/v$RUBYGEMS_VERSION/rubygems-$RUBYGEMS_VERSION.tgz" \
	&& mkdir -p /usr/local/src/rubygems \
	&& tar -zxf /rubygems.tgz -C /usr/local/src/rubygems --strip-components=1 \
	&& rm /rubygems.tgz \
	&& cd /usr/local/src/rubygems \
	&& ruby setup.rb \
	&& cd / \
	&& rm -rf /usr/local/src/rubygems \
	&& apt-get purge -y xz-utils \
	&& apt-mark auto '.*' > /dev/null \
	&& apt-mark manual $savedAptMark \
	&& find /usr/local -type f -executable -not \( -name '*tkinter*' \) -exec ldd '{}' ';' \
		| awk '/=>/ { print $(NF-1) }' \
		| sort -u \
		| xargs -r dpkg-query --search \
		| cut -d: -f1 \
		| sort -u \
		| xargs -r apt-mark manual \
	&& apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
	&& ruby --version \
	&& gem --version

CMD ["irb"]
