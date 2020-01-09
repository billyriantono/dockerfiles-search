FROM debian:8
MAINTAINER Guillaume Bienkowski <gbi@linphone.org>

RUN apt-get update

# all dependencies for building the .deb of flexisip
RUN apt-get -y install alien \
						autoconf \
						automake \
						bison \
						build-essential \
						cmake \
						doxygen \
						git \
						intltool \
						libboost-system1.55-dev \
						libboost1.55-dev \
						libhiredis-dev \
						libmysqlclient-dev \
						libprotobuf-dev \
						libssl-dev \
						libtool \
						pkg-config \
						protobuf-compiler \
						python \
						rpm \
						sudo \
						unixodbc-dev \
						wget

#debian doesn't ship with the %cmake macro of rpmbuild.
ADD .rpmmacros /root/.rpmmacros
