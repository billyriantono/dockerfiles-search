# Base OpenJDK image
# Uses v9.3 of my base image
FROM aemiller/base-debian:9.3
LABEL maintainer="miller@adammiller.io"

ENV DEBIAN_FRONTEND=noninteractive
ENV JAVA_TYPE=jdk
ENV JAVA_VERSION=8u151-b12-1~deb9u1

# Set the correct locale and install java and locales
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
	apt-get update && apt-get install -y \
		openjdk-8-$JAVA_TYPE-headless=$JAVA_VERSION \
	&& rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/usr/bin/java"]
