FROM node:10

RUN apt-get update && apt-get install -y python-pip jq && \
	pip install awscli && \
	rm -rf /var/lib/apt/lists/*

RUN node --version && npm install yarn --global

