FROM debian:stretch-slim

ARG FF_VER=70.0.1
ARG TRIDACTYL_NATIVE_COMMIT=11f29024

ENV LANG C.UTF-8
ENV FF_LANG en-US
ENV FF_FEATURES_PATH /opt/firefox/browser/features

RUN apt-get -y update \
	&& apt-get install -y --no-install-recommends \
	# default fonts don't support CJK langs
	fonts-noto-cjk \
	# for tridactyl native client install script
	python3 curl \
	# install firefox dependencies
	libxt6 libdbus-glib-1-2 libgtk-3-0 ca-certificates bzip2 dirmngr gnupg \
	libasound2 libgl1-mesa-dri libgl1-mesa-glx libxrender1 libx11-xcb-dev \
	libx11-xcb1 libpulse0 libcanberra-gtk3-module \
	$(apt-cache depends firefox-esr | grep Depends | sed "s/.*ends:\ //" | tr '\n' ' ') \
	&& apt-get install -y \
	# codecs for firefox
	ffmpeg \
	# cleanup
	&& rm -rf /var/lib/apt/lists/*

# install firefox
RUN cd /tmp \
	&& curl -sSOL "https://download-installer.cdn.mozilla.net/pub/firefox/releases/${FF_VER}/linux-x86_64/${FF_LANG}/firefox-${FF_VER}.tar.bz2" \
	&& tar -vxj -C /opt -f "firefox-${FF_VER}.tar.bz2" \
	&& rm -rf firefox-${FF_VER}.tar.bz2 \
	# remove firefox "features" and don't let it install any features in the future
	&& mkdir -p "${FF_FEATURES_PATH}" \
	&& rm -rf "${FF_FEATURES_PATH}/*" \
	&& chmod 000 "${FF_FEATURES_PATH}" \
	&& chown root:root "${FF_FEATURES_PATH}" \
	# make directory for policies.json
	&& mkdir /opt/firefox/distribution \
	&& ln -s /opt/firefox/firefox /usr/local/bin/firefox

# better fonts (AA..)
COPY local.conf /etc/fonts/local.conf

# firefox user
RUN adduser --disabled-password user
USER user

# install tridactyl native client
RUN curl -sSL -o /tmp/trinativeinstall.sh \
	https://raw.githubusercontent.com/tridactyl/tridactyl/${TRIDACTYL_NATIVE_COMMIT}/native/install.sh \
	&& bash /tmp/trinativeinstall.sh ${TRIDACTYL_NATIVE_COMMIT}

ENTRYPOINT [ "/usr/local/bin/firefox" ]
