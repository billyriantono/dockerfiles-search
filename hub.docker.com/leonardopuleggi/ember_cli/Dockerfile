FROM node:8.15.1
LABEL Leonardo <leonardo.puleggi@gmail.com>
LABEL description="Based on danlynn https://github.com/danlynn/ember-cli/ and sergiolepore https://github.com/sergiolepore/ Ember CLI Docker Image"

ENV WATCHMAN_VERSION=v4.9.0 EMBER_CLI_VERSION=3.4.4

# ember server on port 4200
# livereload server on port 7020 (changed in v2.17.0 from 49153)
# test server on port 7357
EXPOSE 4200 7020 7357

# Install watchman build dependencies 
RUN \ 
	apt-get update -y &&\
	apt-get install -y python-dev
 
# install watchman
# Note: See the README.md to find out how to increase the
# fs.inotify.max_user_watches value so that watchman will 
# work better with ember projects.
RUN \
	git clone https://github.com/facebook/watchman.git &&\
	cd watchman &&\
	git checkout ${WATCHMAN_VERSION} &&\
	./autogen.sh &&\
	./configure &&\
	make &&\
	make install

# install chrome for default testem config (as of 2.15.0)
RUN \
    apt-get update &&\
    apt-get install -y \
        apt-transport-https \
        gnupg \
        --no-install-recommends &&\
	curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - &&\
	echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list &&\
	apt-get update &&\
	apt-get install -y \
	    google-chrome-stable \
	    --no-install-recommends \
	&&  rm -rf /var/lib/apt/lists/*

# tweak chrome to run with --no-sandbox option
RUN \
	sed -i 's/"$@"/--no-sandbox "$@"/g' /opt/google/chrome/google-chrome

# set container bash prompt color to blue in order to 
# differentiate container terminal sessions from host 
# terminal sessions
RUN \
	echo 'PS1="\[\\e[0;94m\]${debian_chroot:+($debian_chroot)}\\u@\\h:\\w\\\\$\[\\e[m\] "' >> ~/.bashrc

#used to remove old temp folder and Ember CLI
RUN \
	npm install -g rimraf \
	&& npm install -g ember-cli@${EMBER_CLI_VERSION}

#============================================
# OS Cleanup
#============================================
RUN rm -rf /var/cache/apk/* \
      /usr/share/man \
      /tmp/watchman

#============================================
# Default working directory
#============================================
WORKDIR /myapp

#============================================
# Default command to be run
#============================================
CMD ["ember", "server"]
