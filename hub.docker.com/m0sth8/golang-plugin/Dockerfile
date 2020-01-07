FROM dockerfile/java:openjdk-7-jdk
MAINTAINER M0stH8 <m0sth8@gmail.com>

ENV IDEA_VERSION 14.0.1

ADD ./build /build

RUN /build/install.sh

ENTRYPOINT ["/build/build.sh"]