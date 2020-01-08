FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y \
	cmake \
	wget \
	clang \
	libicu-dev \
	libpython2.7-dev \
	pkg-config \
	git-core \
	libssl-dev \
	libcurl4-openssl-dev \
	libbsd-dev

ARG swiftversion=5.0

RUN wget https://swift.org/builds/swift-${swiftversion}-release/ubuntu1804/swift-${swiftversion}-RELEASE/swift-${swiftversion}-RELEASE-ubuntu18.04.tar.gz
RUN tar xvf swift-${swiftversion}-RELEASE-ubuntu18.04.tar.gz
RUN rm swift-${swiftversion}-RELEASE-ubuntu18.04.tar.gz
RUN mv swift-${swiftversion}-RELEASE-ubuntu18.04 /usr/local/bin/swift
RUN echo "export PATH='\$PATH:/usr/local/bin/swift/usr/bin'" >> /root/.bashrc
RUN /usr/local/bin/swift/usr/bin/swift -version
RUN whoami
