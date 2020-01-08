FROM debian

RUN apt-get -y update && apt-get install -y build-essential \
		wget \
		curl \
		git \
		sudo \
		libfontconfig && \
	\
	mkdir /usr/local/nvm && \
	\
	wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.26.1/install.sh \
		| PROFILE=/etc/profile NVM_DIR=/usr/local/nvm sh
