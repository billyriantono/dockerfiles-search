FROM debian:buster

WORKDIR /root
SHELL ["/bin/bash", "-c"]

# Setup the environment
ENV BASH_ENV="/root/.bash_profile"
ENV BUNDLE_SILENCE_ROOT_WARNING=1

# Install dependencies
RUN set -eu; \
	apt-get update; \
	apt-get install -y --no-install-recommends bison build-essential \
		ca-certificates git libgdbm-dev libffi-dev libpq-dev \
		libreadline-dev libssl-dev libyaml-dev openssh-client wget \
		zlib1g-dev

# Install chruby
RUN set -eu; \
	wget -O chruby-0.3.9.tar.gz \
		https://github.com/postmodern/chruby/archive/v0.3.9.tar.gz; \
	tar -xzvf chruby-0.3.9.tar.gz; \
	cd chruby-0.3.9/; \
	make install; \
	cd; \
	rm -r chruby-0.3.9 chruby-0.3.9.tar.gz; \
	printf "source /usr/local/share/chruby/chruby.sh\n" >> /root/.bash_profile

# Install ruby-install
RUN set -eu; \
	wget -O ruby-install-0.7.0.tar.gz \
		https://github.com/postmodern/ruby-install/archive/v0.7.0.tar.gz; \
	tar -xzvf ruby-install-0.7.0.tar.gz; \
	cd ruby-install-0.7.0/; \
	make install; \
	cd; \
	rm -r ruby-install-0.7.0 ruby-install-0.7.0.tar.gz

# Install Ruby
RUN set -eu; \
	ruby-install ruby 2.7.0 --no-install-deps -- --disable-install-rdoc; \
	printf "chruby ruby-2.7.0\n" >> /root/.bash_profile; \
	printf "install: --no-document\nupdate: --no-document\n" >> /root/.gemrc

# Install Yarn
RUN set -eu; \
	apt-get install -y --no-install-recommends yarnpkg; \
	ln -sf /usr/bin/yarnpkg /usr/bin/yarn

RUN set -eu; \
	uname -a; \
	ruby --version; \
	node --version; \
	yarn --version

CMD ["/bin/bash", "-l"]
