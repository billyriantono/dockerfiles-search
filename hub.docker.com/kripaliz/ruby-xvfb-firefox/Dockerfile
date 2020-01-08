FROM ruby:2.3

ARG FIREFOX_VERSION=43.0

RUN apt-get update && \
	apt-get install -y xvfb firefox-esr && \
	apt-get purge -y firefox-esr && \
	wget --no-verbose -O /tmp/firefox.deb sourceforge.net/projects/ubuntuzilla/files/mozilla/apt/pool/main/f/firefox-mozilla-build/firefox-mozilla-build_$FIREFOX_VERSION-0ubuntu1_amd64.deb && \
	dpkg -i /tmp/firefox.deb && \
	rm -rf /var/lib/apt/lists/* && \
	rm /tmp/firefox.deb
