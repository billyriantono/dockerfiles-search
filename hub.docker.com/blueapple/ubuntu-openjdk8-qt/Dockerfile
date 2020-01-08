FROM phusion/baseimage
MAINTAINER blueapple <blueapple1120@qq.com>

RUN apt-get -y update && apt-get install -y --no-install-recommends \
		build-essential \
		libgl1-mesa-dev \
		cmake \
		doxygen \
		graphviz \
		pkg-config \
		qt5-default \
		libqt5sql5-odbc \
		libqt5sql5-psql \
		openjdk-8-jdk \
		openjdk-8-jdk-headless\
		sudo \
	&& echo 'qt ALL=(ALL) NOPASSWD: ALL' >/etc/sudoers.d/qt \
	&& rm -rf /var/lib/apt/lists/*

# Set java environment
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV PATH $PATH:/usr/lib/jvm/java-8-openjdk-amd64/jre/bin:/usr/lib/jvm/java-8-openjdk-amd64/bin

RUN useradd -m -d /home/qt qt
USER qt
ENV HOME=/home/qt
WORKDIR /home/qt
CMD ["/bin/bash"]
