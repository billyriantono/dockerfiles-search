# nodejs
#
# VERSION: latest (unstable)

FROM ubuntu
MAINTAINER Nathan Tran <ntran013@gmail.com>

# Update dependencies
RUN apt-get -y update \
		&& apt-get -y install \
			git-core \
			curl \
			wget \
			make

# install node latest (unstable)
RUN git clone https://github.com/visionmedia/n.git /opt/n \
		&& cd /opt/n \
		&& make install \
		&& n latest