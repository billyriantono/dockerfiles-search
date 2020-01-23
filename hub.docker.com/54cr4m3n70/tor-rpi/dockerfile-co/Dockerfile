# Based on the yenpai/jetbrains-clion 

FROM 4emodan/jvm-gui:latest
MAINTAINER Artyom Lonsky <artyom.lonsky@gmail.com>

# Install clion and build tools
RUN export cl_version="CLion-2016.2" && \
	apt-get update -qy && \
	apt-get install -qy --no-install-recommends \
		build-essential autoconf automake \
		git subversion && \
	apt-get clean && \
	apt-get autoremove -qy && \
	rm -rf /var/lib/apt/lists/* && \
	wget --output-document=/tmp/clion.tar.gz \
		--no-check-certificate --no-cookies \
		http://download.jetbrains.com/cpp/${cl_version}.tar.gz && \
	mkdir -p /opt/clion && \
	tar zxvf /tmp/clion.tar.gz --strip-components=1 -C /opt/clion && \
	rm -f /tmp/*

# Setup Path
ENV CL_JDK="/usr/lib/jvm/oracle-jdk-8" \
	HOME="/home/developer" \
	WORKSPACE="/work"

# Create workspace/home, add group/account, sudo
RUN export uid=1000 gid=1000 && \
	mkdir -p ${WORKSPACE} && mkdir -p ${HOME} && \
	echo "developer:x:${uid}:${gid}:Developer,,,:${HOME}:/bin/bash" >> /etc/passwd && \
	echo "developer:x:${uid}:" >> /etc/group && \
	echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
	chmod 0440 /etc/sudoers.d/developer && \
	chown ${uid}:${gid} -R ${HOME}

# USER, WORKDIR, ENTRYPOINT
USER developer:developer
WORKDIR $WORKSPACE
ENTRYPOINT ["/opt/clion/bin/clion.sh"]