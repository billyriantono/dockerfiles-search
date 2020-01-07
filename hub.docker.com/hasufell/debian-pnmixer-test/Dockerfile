FROM debian:stable

ENV DEBIAN_FRONTEND=noninteractive

# update the package repositories
RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y wget curl locales && \
	echo "Europe/Stockholm" > /etc/timezone && \
	dpkg-reconfigure -f noninteractive tzdata && \
	export LANGUAGE=en_US.UTF-8 && \
	export LANG=en_US.UTF-8 && \
	export LC_ALL=en_US.UTF-8 && \
	locale-gen en_US.UTF-8 && \
	dpkg-reconfigure locales && \
	apt-get install -y libgtk-3-0 libgtk-3-bin libgtk-3-dev libgtk-3-common \
		libgtk2.0 libgtk2.0-bin libgtk2.0-cil libgtk2.0-cil-dev \
		libgtk2.0-common libgtk2.0-dev \
		libx11-6 libx11-data libx11-dev \
		libglib2.0-0 libglib2.0-bin libglib2.0-cil libglib2.0-cil-dev \
		libglib2.0-data libglib2.0-dev \
		libnotify-bin libnotify-cil-dev libnotify-dev \
		intltool gettext pkg-config automake autoconf \
		libasound2 libasound2-data libasound2-dev \
		clang && \
	rm -rf /var/lib/apt/lists && \
	apt-get autoremove -y && \
	apt-get clean
