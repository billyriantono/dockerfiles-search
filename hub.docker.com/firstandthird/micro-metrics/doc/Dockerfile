FROM firekcc/alpine-glibc
MAINTAINER firekcc <lyk_1226@126.com>

# server-jre-1.8.0_211
ADD jre8.tar.gz /opt/jdk/

# set env
ENV JAVA_HOME /opt/jdk
ENV PATH ${PATH}:${JAVA_HOME}/bin

WORKDIR /opt
CMD ["/bin/sh"]
