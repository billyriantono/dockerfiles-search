#
# AAAL Development Environment
#

FROM nvidia/cudagl:9.2-devel-ubuntu18.04
LABEL maintainer="Tarek Taha <tarek.taha@algorythma.com>"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y --quiet --no-install-recommends install \
		sudo \
		nano \
		net-tools \
		iputils-* \
		bash-completion \
		autotools-dev \
		dh-autoreconf \
		bzip2 \
		ca-certificates \
		ccache \
		cmake \
		cppcheck \
		curl \
		dirmngr \
		doxygen \
		file \
		g++ \
		gcc \
		gdb \
		git \
		gnupg \
		gosu \
		lcov \
		libfreetype6-dev \
		libgtest-dev \
		libpng-dev \
		lsb-release \
		make \
		ninja-build \
		openjdk-8-jdk \
		openjdk-8-jre \
		openssh-client \
		pkg-config \
		python-pip \
		python-pygments \
		python-setuptools \
		python-wstool \
		locate \
		rsync \
		shellcheck \
		tzdata \
		unzip \
		wget \
		xsltproc \
		zip \
	&& apt-get -y autoremove \
	&& apt-get clean autoclean \
	&& rm -rf /var/lib/apt/lists/{apt,dpkg,cache,log} /tmp/* /var/tmp/*

# gtest
RUN cd /usr/src/gtest \
	&& mkdir build && cd build \
	&& cmake .. && make \
	&& cp *.a /usr/lib \
	&& cd .. && rm -rf build

RUN python -m pip install --upgrade pip \
	&& pip install setuptools pkgconfig wheel \
	&& pip install argparse argcomplete coverage jinja2 empy numpy requests serial toml pyyaml cerberus

# manual ccache setup
#RUN ln -s /usr/bin/ccache /usr/lib/ccache/cc \
#	&& ln -s /usr/bin/ccache /usr/lib/ccache/c++

# astyle v2.06
RUN wget -q https://downloads.sourceforge.net/project/astyle/astyle/astyle%202.06/astyle_2.06_linux.tar.gz -O /tmp/astyle.tar.gz \
	&& cd /tmp && tar zxf astyle.tar.gz && cd astyle/src \
	&& make -f ../build/gcc/Makefile && cp bin/astyle /usr/local/bin \
	&& rm -rf /tmp/*

# create aaal with id 1000 with sudo access
RUN useradd --shell /bin/bash -u 1000 -c "" -m aaal && usermod -a -G dialout aaal && echo "aaal:aaal" | chpasswd && adduser aaal sudo
RUN sed -i '/force_color_prompt/s/^#//g' ~/.bashrc
RUN sed -i '/force_color_prompt/s/^#//g' /home/aaal/.bashrc

# setup virtual X server
RUN mkdir /tmp/.X11-unix && \
	chmod 1777 /tmp/.X11-unix && \
	chown -R root:root /tmp/.X11-unix
ENV DISPLAY :99

ENV CCACHE_UMASK=000
ENV FASTRTPSGEN_DIR="/usr/local/bin/"
ENV PATH="/usr/lib/ccache:$PATH"
ENV TERM=xterm
ENV TZ=UTC

# SITL UDP PORTS
EXPOSE 14556/udp
EXPOSE 14557/udp

CMD ["/bin/bash"]
