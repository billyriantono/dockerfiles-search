FROM debian:testing
MAINTAINER Jesper Utoft <jesper@utoft.org>

RUN apt-get update && apt-get install -y --no-install-recommends \
	openjdk-8-jre-dcevm=8u112-1 \
	openjdk-8-jdk-headless=8u111-b14-3 \
	&& rm -rf /var/lib/apt/lists/*