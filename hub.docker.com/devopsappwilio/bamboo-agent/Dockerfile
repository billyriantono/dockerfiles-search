FROM atlassian/bamboo-base-agent:latest

RUN echo "deb http://archive.ubuntu.com/ubuntu/ trusty-proposed main restricted universe multiverse" >> /etc/apt/sources.list \
	&& echo "deb http://archive.ubuntu.com/ubuntu/ trusty-backports main restricted universe multiverse" >> /etc/apt/sources.list \
	&& echo "deb http://archive.ubuntu.com/ubuntu/ trusty main restricted universe multiverse" >> /etc/apt/sources.list

RUN apt-get update && apt-get install -yf \
	language-pack-ru \
	curl \
	git \
	software-properties-common \
	libgtk2.0-0 \
	libgconf-2-4 \
	libasound2 \
	libxtst6 \
	libxss1 \
	libnss3 \
	xvfb \
	xfonts-100dpi \
	xfonts-75dpi \
	xfonts-scalable \
	xfonts-cyrillic \
	zip

ENV LANGUAGE ru_RU.UTF-8
ENV LANG ru_RU.UTF-8
ENV LC_ALL ru_RU.UTF-8
RUN locale-gen ru_RU.UTF-8 && dpkg-reconfigure locales

RUN curl -sL https://deb.nodesource.com/setup_6.x -o /tmp/nodesource_setup.sh \
	&& bash /tmp/nodesource_setup.sh && apt-get install -yf nodejs
#RUN apt-get install -yf default-jdk
RUN add-apt-repository ppa:webupd8team/java \
	&& apt-get update \
	&& echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
	&& echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections \
	&& apt-get install -yf oracle-java8-installer \
	&& apt-get install -yf oracle-java8-set-default \
	&& export JAVA_HOME=/usr/lib/jvm/java-8-oracle \
	&& export PATH=$JAVA_HOME/bin:$PATH
