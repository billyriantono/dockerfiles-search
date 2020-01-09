FROM ubuntu:xenial
MAINTAINER Nagendra <ndonthi@next-level-integration.com>

ENV DEBIAN_FRONTEND=noninteractive \ 
    JAVA_HOME=/usr/lib/jvm/java-8-oracle \ 
    JRE_HOME=/usr/lib/jvm/java-8-oracle/jre

RUN VERSION=8 && \ 
    UPDATE=181 && \ 
	BUILD=13 && \ 
	SIG=96a7b8442fe848ef90c96a2fad6ed6d1 && \
    apt-get update && apt-get dist-upgrade -y && \ 
	apt-get install apt-utils ca-certificates curl -y --no-install-recommends && \ 
	curl --silent --location --retry 3 --cacert /etc/ssl/certs/GeoTrust_Global_CA.pem \ 
	--header "Cookie: oraclelicense=accept-securebackup-cookie;" \ 
	http://download.oracle.com/otn-pub/java/jdk/"${VERSION}"u"${UPDATE}"-b"${BUILD}"/"${SIG}"/jdk-"${VERSION}"u"${UPDATE}"-linux-x64.tar.gz \ 
	| tar xz -C /tmp && \
    mkdir -p /usr/lib/jvm && mv /tmp/jdk1.${VERSION}.0_${UPDATE} "${JAVA_HOME}" && \ 
	apt-get autoclean && apt-get --purge -y autoremove && \ 
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \ 
	update-alternatives --install "/usr/bin/java" "java" "${JRE_HOME}/bin/java" 1 && \ 
	update-alternatives --install "/usr/bin/javaws" "javaws" "${JRE_HOME}/bin/javaws" 1 && \ 
	update-alternatives --install "/usr/bin/javac" "javac" "${JAVA_HOME}/bin/javac" 1 && \ 
	update-alternatives --set java "${JRE_HOME}/bin/java" && \ 
	update-alternatives --set javaws "${JRE_HOME}/bin/javaws" && \ 
	update-alternatives --set javac "${JAVA_HOME}/bin/javac"
RUN apt-get -qq update && \
    apt-get -q -y upgrade && \
    apt-get install -y sudo curl wget locales && \
    rm -rf /var/lib/apt/lists/*
RUN apt-get update  
