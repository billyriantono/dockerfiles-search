FROM node:8.11.2

# Set environment variables
ENV \
	BABEL_VERSION=latest

ENV \
	GULP_VERSION=latest

ENV \
	GRUNT_VERSION=latest

ENV \
	WEBPACK_CLI_VERSION=latest

ENV \
	YARN_VERSION=stable

# Run updates
RUN \
	echo -e "\nRunning apt-get update..." && \
	apt-get update

# Install curl
RUN \
	echo -e "\nInstalling curl..." && \
	apt-get install -y curl

# Install Node 8
RUN \
	echo -e "\nInstalling Node 8..." && \
	curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
	apt-get install -y nodejs

# Install wget
RUN \
	echo -e "\nInstalling wget..." && \
	apt-get install -y wget


# Install openssl
RUN \
	echo -e "\nInstalling openssl..." && \
	apt-get install -y openssl

# Install git
RUN \
	echo -e "\nInstalling git..." && \
	apt-get install -y git

# Install ssh
RUN \
	echo -e "\nInstalling ssh..." && \
	apt-get install -y ssh

# Install rsync
RUN \
	echo -e "\nInstalling rsync..." && \
	apt-get install -y rsync

# Update npm
RUN \
	echo -e "\nUpdating npm..." && \
	npm install -g npm@latest

# Install babel-register globally
RUN \
	echo -e "\nInstalling babel-register v${BABEL_VERSION}..." && \
	npm install -g babel-register@${BABEL_VERSION}

# Install gulp globally
RUN \
	echo -e "\nInstalling gulp v${GULP_VERSION}..." && \
	npm install -g gulp@${GULP_VERSION}

# Install grunt globally
RUN \
	echo -e "\nInstalling grunt v${GRUNT_VERSION}..." && \
	npm install -g grunt@${GRUNT_VERSION}

# Install webpack globally
RUN \
	echo -e "\nInstalling webpack v${WEBPACK_CLI_VERSION}..." && \
	npm install -g webpack-cli@${WEBPACK_CLI_VERSION}

# Install yarn globally
RUN \
	echo "Installing yarn v${YARN_VERSION}..." && \
	curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -  && \
	echo "deb https://dl.yarnpkg.com/debian/ ${YARN_VERSION} main" | tee /etc/apt/sources.list.d/yarn.list  && \
	apt-get update && apt-get --no-install-recommends install yarn
