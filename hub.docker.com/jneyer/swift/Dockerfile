FROM ubuntu:16.04
MAINTAINER John Neyer <github@jneyer.com>
ENV SWIFT_RELEASE=https://swift.org/builds/swift-3.1-release/ubuntu1604/swift-3.1-RELEASE/swift-3.1-RELEASE-ubuntu16.04.tar.gz

RUN apt-get update && apt-get -y upgrade \
&& apt-get -y install curl clang libicu-dev libpython2.7-dev libxml2-dev \
&& cd /tmp \
&& curl $SWIFT_RELEASE -o swift.tgz \
&& curl -q https://swift.org/keys/all-keys.asc | gpg --import - \ 
&& curl $SWIFT_RELEASE.sig -o swift.tgz.sig \
&& gpg --verify swift.tgz.sig \
&& tar zxvf swift.tgz \
&& mv swift-*/usr /usr/local/swift \
&& ln -s /usr/local/swift/bin/* /usr/local/bin

