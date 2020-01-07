FROM python:3.7-slim

RUN apt-get update && \
	apt-get install -y curl && \
	curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash && \
	. /root/.bashrc && \
	nvm install v10 && \
	ln -s $(which npm) /usr/local/bin/npm && \
	ln -s $(which node) /usr/local/bin/node

