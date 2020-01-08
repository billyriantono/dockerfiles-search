FROM ubuntu
MAINTAINER Hubert Dworczyński <hubert.dworczynski@gmail.com>

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get update && apt-get install -y \
	nodejs \
	make \
	tree \
	g++ \
	gnupg \
	firefox \
	google-chrome-stable \
	default-jre	

RUN npm install -g \
	polymer-cli \
	web-component-tester \
	wct-headless \
	bower \
	gulp
