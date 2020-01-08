FROM pbarnoux/oraclejdk-minimal
MAINTAINER Pierre Barnoux <pbarnoux@gmail.com>

# Maven and Node versions
ENV MVN_VER="3.3.3" NODE_VER="v0.12.7"

# Install required dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
	bzip2 \
	g++ \
	git \
	# Run grunt test (karma + phantomjs)
	libfontconfig \
	make \
	nasm \
	python && \
# Download maven and node as tarballs (seems to save space)
	curl -qo /tmp/maven.tar.gz http://apache.mirrors.ovh.net/ftp.apache.org/dist/maven/maven-3/${MVN_VER}/binaries/apache-maven-${MVN_VER}-bin.tar.gz && \
	curl -qo /tmp/node.tar.gz https://nodejs.org/dist/${NODE_VER}/node-${NODE_VER}-linux-x64.tar.gz && \
# Uncompress tarballs
	tar zxvf /tmp/maven.tar.gz -C /usr/local && \
	tar zxvf /tmp/node.tar.gz -C /usr/local && \
# Create links for package installed from tarballs
	ln -s /usr/local/*maven*/bin/mvn /usr/bin/mvn && \
	ln -s /usr/local/node*/bin/node /usr/bin/node && \
	ln -s /usr/local/node*/bin/npm /usr/bin/npm && \
# Install npm dependencies
	npm install -g --allow-root yo bower grunt-cli gulp generator-angular && \
# yo falls back to a non-root user while running
	mkdir -p /root/.config/configstore && \
	chmod 777 /root /root/.config /root/.config/configstore && \
# Clean various caches
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /tmp/* /var/tmp/*

CMD ["/bin/bash"]

