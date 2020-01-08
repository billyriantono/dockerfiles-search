FROM tcloud/ubuntu-python:latest
MAINTAINER tcloud

USER root

ENV DEBIAN_FRONTEND="noninteractive" \
	JDK_VERSION=9 \
	LC_ALL="en_US.UTF-8" \
	JAVA_HOME="/usr/lib/jvm/default-java"

RUN (echo "en_US ISO-8859-1" && echo "en_US.UTF-8 UTF-8") > /etc/locale.gen && locale-gen && \
	sed -i.bak 's/main$/main universe/' /etc/apt/sources.list && \
	apt-get -qq update && \
    apt-get -y install \
    	apt-utils \
	    locales \
	    curl \
	    wget \
	    vim \
	    build-essential \
	    zip \
	    unzip \
	    libc6 \
	    libstdc++6 \
	    libcups2 \
	    liblcms2-2 \
	    libjpeg8 \
	    libnss3 \
	    libfontconfig1 \
	    libfreetype6 \
	    libglib2.0-0 \
	    libkrb5-3 \
	    libpcsclite1 \
	    zlib1g \
	    ttf-dejavu-extra \
	    software-properties-common \
	    && \
	add-apt-repository ppa:webupd8team/java && \
	apt-get -qq update && \
	echo oracle-java${JDK_VERSION}-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
	apt-get -qq -y install oracle-java${JDK_VERSION}-installer && \
	apt-get -y install oracle-java${JDK_VERSION}-set-default && \
	ln -s /usr/lib/jvm/java-${JDK_VERSION}-oracle /usr/lib/jvm/default-java && \
	update-alternatives --display java && \
	echo "JAVA_HOME=${JAVA_HOME}">> /etc/environment && \
	echo "PATH=$JAVA_HOME/bin:$PATH">> /etc/environment

CMD ["/sbin/my_init"]

# Clean up
RUN apt-get clean && \
	apt-get autoremove -y && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*