FROM ubuntu

RUN apt-get update
RUN apt-get install -y \
	curl \
	openjdk-8-jdk \
	firefox \
	language-pack-de-base

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
