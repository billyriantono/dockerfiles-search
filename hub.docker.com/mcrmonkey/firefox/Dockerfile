FROM debian:sid
MAINTAINER ant <git@manchestermonkey.co.uk>


ENV LANG en-US
ENV HOME /home/firefox

RUN apt-get update -qq && apt-get install -qq \
	dirmngr \
	gnupg \
	--no-install-recommends \
	&& apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 0AB215679C571D1C8325275B9BDB3D89CE49EC21 \
	&& echo "deb http://ppa.launchpad.net/mozillateam/firefox-next/ubuntu wily main" >> /etc/apt/sources.list.d/firefox.list \
	&& apt-get update -qq && apt-get install -qq ca-certificates firefox libcanberra-gtk-module 	hicolor-icon-theme libasound2 libgl1-mesa-dri libgl1-mesa-glx --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* \
	&& useradd --create-home --home-dir $HOME firefox \
	&& gpasswd -a firefox audio \
	&& chown -R firefox:firefox $HOME


COPY local.conf /etc/fonts/local.conf


WORKDIR $HOME
USER firefox


ENTRYPOINT [ "/usr/bin/firefox" ]
