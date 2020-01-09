FROM atlassian/default-image:latest

RUN \
  # add repo
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -

RUN \  
  # install yarn
  curl -o- -L https://yarnpkg.com/install.sh | bash

RUN \
	# install n for node update
	npm install -g n

RUN \
	# fix on version of node
    n 7.4.0

ENV PATH "/usr/local/n/versions/node/7.4.0/bin:$PATH:$HOME/.yarn/bin"
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
CMD ["bash"]