FROM selenium/node-chrome:2.52.0

USER root

RUN set -x \
	&& apt-get update \
	&& apt-get install -y openjdk-8-jdk \
	&& rm -rf /var/lib/apt/lists/*
	
# see https://bugs.debian.org/775775
# and https://github.com/docker-library/java/issues/19#issuecomment-70546872
RUN update-ca-certificates -f