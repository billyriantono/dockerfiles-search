FROM aoowweenn/trusty-jdk7
MAINTAINER Owen Chien <aoowweenn@gmail.com>
RUN dpkg --add-architecture i386 \
	&& apt-get update
RUN apt-get --no-install-recommends -y --force-yes install autoconf2.13 bison bzip2 ccache curl flex gawk gcc g++ g++-multilib gcc-4.7 g++-4.7 g++-4.7-multilib git lib32ncurses5-dev lib32z1-dev zlib1g:amd64 zlib1g-dev:amd64 zlib1g:i386 zlib1g-dev:i386 libgl1-mesa-dev libx11-dev make zip libxml2-utils lzop \
	python libfontconfig1 libxrender1 libxcomposite1 libasound2 \
	libdbus-glib-1-2 libgtk2.0-0 libxt6 unzip \
	libglapi-mesa:i386 libgl1-mesa-glx:i386
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.7 1 \
	&& update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 2 \
	&& update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.7 1 \
	&& update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 2 \
	&& update-alternatives --set gcc "/usr/bin/gcc-4.7" \
	&& update-alternatives --set g++ "/usr/bin/g++-4.7"
RUN apt-get clean \
	&& rm -f /var/lib/apt/lists/*_dists_* \
	&& ccache --max-size 10GB \
	&& git config --global user.email "abc@abc.com" \
	&& git config --global user.name "abc" \
	&& cd /home \
	&& git clone git://github.com/mozilla-b2g/B2G.git
CMD export SHELL=/bin/bash \
	&& cd /home/B2G
