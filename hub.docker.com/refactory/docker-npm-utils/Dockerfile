FROM node:8-slim

RUN npm install --production --loglevel warn -g eslint eslint-config-standard eslint-plugin-compat eslint-plugin-promise eslint-plugin-standard eslint-plugin-import@latest eslint-plugin-node@latest > /dev/null

WORKDIR /home/node
USER root

# install chrome for default testem config (as of 2.15.0)
RUN \
    apt-get update &&\
    apt-get install -y \
        apt-transport-https \
	rsync \
	git \
	bzip2 \
        gnupg \
	openssh-client \
        --no-install-recommends &&\
	curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - &&\
	echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list &&\
	apt-get update &&\
	apt-get install -y \
	    google-chrome-stable \
	    --no-install-recommends

# tweak chrome to run with --no-sandbox option
RUN \
	sed -i 's/"$@"/--no-sandbox "$@"/g' /opt/google/chrome/google-chrome

# install watchman
# Note: See the README.md to find out how to increase the
# fs.inotify.max_user_watches value so that watchman will 
# work better with ember projects.
# RUN \
# 	ap
# 	git clone https://github.com/facebook/watchman.git &&\
# 	cd watchman &&\
# 	git checkout v4.9.0 &&\
# 	./autogen.sh &&\
# 	./configure &&\
# 	make &&\
# 	make install

# set container bash prompt color to blue in order to 
# differentiate container terminal sessions from host 
# terminal sessions
RUN \
	echo 'PS1="\[\\e[0;94m\]${debian_chroot:+($debian_chroot)}\\u@\\h:\\w\\\\$\[\\e[m\] "' >> ~/.bashrc

# install ember-cli
RUN \
	npm install -g ember-cli@3.3.0

# install phantomjs
RUN \
	yarn global add phantomjs-prebuilt

# install gulp
RUN npm i -g gulp && \
    rm -rf /tmp/*

CMD ["/bin/bash", "ember", "server", "gulp"]
