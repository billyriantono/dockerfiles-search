FROM ubuntu

ENV LANG=C.UTF-8

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends python-minimal software-properties-common ca-certificates g++ git curl libevent-dev libncurses-dev make wget gnupg; \
	curl -sL https://deb.nodesource.com/setup_10.x | bash -; \
	apt-get install -y --no-install-recommends nodejs; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 

RUN mkdir /tmux
WORKDIR /tmux

RUN set -eux; \
	wget https://github.com/tmux/tmux/releases/download/2.2/tmux-2.2.tar.gz; \
	tar xvzf tmux-2.2.tar.gz; \
	cd tmux-2.2/; \
	./configure; \
	make; \
	make install 

RUN git clone https://github.com/c9/core.git /cloud9
WORKDIR /cloud9
RUN scripts/install-sdk.sh

RUN mkdir /workspace
VOLUME /workspace

ENV C9_USER= \
	C9_PASSWORD=

EXPOSE 80

ENTRYPOINT nodejs server.js -w /workspace --auth $C9_USER:$C9_PASSWORD --listen 0.0.0.0 --port 80 --collab