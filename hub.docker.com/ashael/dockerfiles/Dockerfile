FROM golang
MAINTAINER Eduardo Arango <eduardo@sylabs.io>

WORKDIR /go/src/github.com/sylabs/singularity 

# install the basics first
RUN apt-get update; \
	apt-get install -y \
		build-essential \
		libssl-dev \
		uuid-dev \
		libgpgme11-dev \
		squashfs-tools \
		libseccomp-dev \
		pkg-config \
		jq
	
RUN git clone https://github.com/sylabs/singularity.git . \
	&& git checkout v3.0.3;
	
RUN ./mconfig \
		&& make -C builddir/ \
		&& make -C builddir/ install;
