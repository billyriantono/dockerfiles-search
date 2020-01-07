# Based on https://github.com/gorelikov/graalvm-maven-gradle-docker
# that is licensed under Apache License 2.0
FROM findepi/graalvm:19.2.0-all
LABEL maintainer="Kevin Röbert <dev@roebert.eu>"

RUN  apt-get install -y \
	curl \
	zip	\
	unzip \
	&& rm -rf /var/lib/apt/lists/*
RUN curl -s "https://get.sdkman.io" | bash
RUN /bin/bash -c "source /root/.sdkman/bin/sdkman-init.sh \
				&& sdk install maven \
				&& sdk install gradle "
