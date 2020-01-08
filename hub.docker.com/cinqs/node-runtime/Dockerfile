FROM google/debian:wheezy

# Install node.js v0.12.0
RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates
RUN mkdir /nodejs && curl http://nodejs.org/dist/v0.12.0/node-v0.12.0-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1

ENV PATH $PATH:/nodejs/bin

# Install npm global packages
RUN npm install pm2@latest -g && \
	npm install coffee-script -g

# Expose monitoring ports
EXPOSE 43554