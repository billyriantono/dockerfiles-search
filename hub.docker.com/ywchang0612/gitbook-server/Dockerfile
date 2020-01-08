FROM debian

MAINTAINER ywchang0612 d60414@gmail.com

RUN apt-get -y update

# Install dependencies
RUN apt-get install -y curl gnupg && \
	curl -sL https://deb.nodesource.com/setup_11.x | bash - && \
	apt-get install -y nodejs && \
	npm install -g gitbook-cli

RUN apt-get purge -y curl gnupg
RUN apt-get autoremove -y
RUN apt-get clean
# Install latest version

RUN mkdir /gitbook
WORKDIR /gitbook

RUN gitbook init

EXPOSE 4000 35729

CMD ["gitbook", "serve", "/gitbook"]
