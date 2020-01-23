FROM amarkwalder/cdk-base:0.1.1
MAINTAINER André Markwalder <andre.markwalder@gmail.com>

ENV     JAVA_VERSION_MAJOR=7 \
	JAVA_VERSION_MINOR=80 \
	JAVA_VERSION_BUILD=15 \
	JAVA_PACKAGE=server-jre
ENV	DOWNLOAD_URL=http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz

WORKDIR	/tmp

RUN	curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie" "${DOWNLOAD_URL}" | gunzip -c - | tar -xf - && \
	mkdir -p /usr/lib/jvm/ && \
	mv jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR}/jre /usr/lib/jvm/jre1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR}/ && \
	rm -rf jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} && \
	ln -s /usr/lib/jvm/jre1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /usr/lib/jvm/jre

WORKDIR	/

ENV	JAVA_HOME=/usr/lib/jvm/jre
ENV	PATH=${PATH}:${JAVA_HOME}/bin

RUN	java -version
