FROM stbuehler/debian-testing-build-essential

MAINTAINER Stefan Bühler <stbuehler@lighttpd.net>

# add gpg key and list file for build.opensuse.org/home:stbuehler (for fcgi-cgi)
COPY obs-home-stbuehler.gpg /etc/apt/trusted.gpg.d/
COPY obs-home-stbuehler.list /etc/apt/sources.list.d/

# adduser + build user with uid/gid 20001
RUN apt-get update \
	&& apt-get install -y \
		adduser \
	&& addgroup --gid 20001 build \
	&& adduser --uid 20001 --gid 20001 --disabled-password --gecos "" build

# git + devscripts + fakeroot + lintian + build deps
# ruby + some gems, libxml2-utils and rsync
RUN apt-get install -y \
		git \
		devscripts \
		fakeroot \
		lintian \
		dh-autoreconf \
		debhelper \
		autotools-dev \
		cmake \
		libev-dev \
		ragel \
		libglib2.0-dev \
		liblua5.1-dev \
		zlib1g-dev \
		libbz2-dev \
		pkg-config \
		libssl-dev \
		libgnutls28-dev \
		libidn11-dev \
		libunwind8-dev \
		cdbs \
		python \
		python-pycurl \
		fcgi-cgi \
		ruby ruby-nokogiri ruby-bluecloth ruby-redcloth \
		libxml2-utils \
		rsync

USER build
