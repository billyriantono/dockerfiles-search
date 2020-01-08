FROM google/debian:wheezy
MAINTAINER Ethan Sebban (ethan.sebban@gmail.com)

# Apt-get initial installs
RUN apt-get update -y && \
	apt-get install --no-install-recommends -y -q git wget curl python build-essential ca-certificates supervisor && \
	mkdir -p /var/log && \
	mkdir -p /etc/supervisor/conf.d/

# Install node.js v0.12.0
RUN mkdir /nodejs && \
	curl http://nodejs.org/dist/v0.12.0/node-v0.12.0-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1
ENV PATH $PATH:/nodejs/bin

# Install npm global packages
RUN npm install pm2@latest -g

# Install new relic server monitoring
RUN echo deb http://apt.newrelic.com/debian/ newrelic non-free >> /etc/apt/sources.list.d/newrelic.list && \
	wget -O- https://download.newrelic.com/548C16BF.gpg | apt-key add - && \
	apt-get update && \
	apt-get install -y -q newrelic-sysmond