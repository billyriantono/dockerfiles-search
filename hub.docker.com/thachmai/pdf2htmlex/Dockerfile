#Dockerfile to build a pdf2htmlEx image

FROM ubuntu

#
#Install git and all dependencies
#Clone the pdf2htmlEX fork of fontforge
#compile it
#Install poppler utils
#Clone and install the pdf2htmlEX git repo
RUN \
	apt-get update \
	&& apt-get install -qq git cmake autotools-dev libjpeg-dev libtiff4-dev libpng12-dev libgif-dev libxt-dev autoconf automake libtool bzip2 libxml2-dev libuninameslist-dev libspiro-dev python-dev libpango1.0-dev libcairo2-dev chrpath uuid-dev uthash-dev \
	&& git clone https://github.com/coolwanglu/fontforge.git fontforge.git \
	&& cd fontforge.git \
	&& git checkout pdf2htmlEX \
	&& ./autogen.sh \
	&& ./configure \
	&& make V=1 \
	&& make install \
	&& apt-get install -qq libpoppler-glib-dev \
	&& echo "Cleaning up" \
	&& rm -rf \var\cache\archives\* \
	&& git clone https://github.com/coolwanglu/pdf2htmlEX.git \
	&& cd pdf2htmlEX \
	&& cmake . \
	&& make \
	&& make install \
	&& mkdir /src

WORKDIR /src
ENTRYPOINT ["/usr/local/bin/pdf2htmlEX"]
