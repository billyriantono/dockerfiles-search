# Based on the dockerfile from Kurron/docker-clion
# Follows guidance from http://www.projectatomic.io/docs/docker-image-author-guidance/
# Base image off of the official Ubuntu-based image
FROM azul/zulu-openjdk:8

ENV DOCKER_VERSION=18.03.0-ce
ENV COMPOSE_VERSION=1.21.0

MAINTAINER Grant Rolls <grantr90@gmail.com> 
USER root

# Create non-root user -- many systems default to 1000 so we'll do that here to make things compatible
RUN groupadd --system powerless --gid 1000 && \
    useradd --uid 1000 --system --gid powerless --home-dir /home/powerless --create-home --shell /sbin/nologin --comment "Docker image user" powerless && \
    chown -R powerless:powerless /home/powerless

# default to being in the user's home directory
WORKDIR /home/powerless

# Set standard Java environment variables
ENV JAVA_HOME /usr/lib/jvm/zulu-8-amd64
ENV JDK_HOME /usr/lib/jvm/zulu-8-amd64

# have Ansible examine the container, by default
CMD ["/usr/bin/ansible", "all", "--inventory=localhost,", "--verbose", "--connection=local", "-m setup"]

# ---- watch your layers and put likely mutating operations here -----

# We need cURL to grab the Docker bits
RUN apt-get -qq update && \
    apt-get -qqy install curl

# Build tools and IDEs need SCMs
RUN apt-get -qq update && \
    apt-get -qqy install git subversion

# IDEs running inside container need these
RUN apt-get -qq update && \
    apt-get -qqy install libgnomevfs2-0 libsecret-1-0 gnome-keyring

# Install Docker client so we can build images and run automated tests 
RUN curl --fail --silent --show-error --location --remote-name https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz && \
    tar --strip-components=1 -xvzf docker-${DOCKER_VERSION}.tgz -C /usr/local/bin && \
    rm -f docker-${DOCKER_VERSION}.tgz && \
    chmod 0555 /usr/local/bin/docker

# Install Docker Compose so we can build images and run automated tests 
RUN curl --fail --silent --show-error --location "https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" --output /usr/local/bin/docker-compose && \
    chmod 0555 /usr/local/bin/docker-compose

# Install Ansible so we can run launch scripts during automated testing
RUN apt-get install --yes software-properties-common && \
    apt-add-repository --yes ppa:ansible/ansible && \
    apt-get update --yes && \
    apt-get install --yes ansible

ENV CL_JDK /usr/lib/jvm/zulu-8-amd64

# Install make and compilers
RUN apt-get update && \
    apt-get install -y \
		build-essential \
		autoconf \
		automake \
		wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

#CLION version and location
ARG CLION_VER=2018.1.3
ARG CLION_TAR=CLion-$CLION_VER.tar.gz
ARG DOWNLOAD_PATH=https://download.jetbrains.com/cpp/$CLION_TAR
ENV CLION_HOME=/opt/clion-$CLION_VER

#Can speed up test/debug by using local tar
#COPY $CLION_TAR /opt/$CLION_TAR
WORKDIR /opt
RUN wget $DOWNLOAD_PATH && \
	mkdir $CLION_HOME && \
	tar -xvf $CLION_TAR && \ 
	rm -rf $CLION_HOME/jre64

RUN chmod 775 $CLION_HOME/bin/clion.sh

#If child image requires root, remember to switch back to non-root 
USER powerless
ENTRYPOINT $CLION_HOME/bin/clion.sh 
