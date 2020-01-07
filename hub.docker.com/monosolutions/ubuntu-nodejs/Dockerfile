# Pull base image.
FROM ubuntu:16.04

# Install Node.js
RUN apt-get update -y && apt-get upgrade -y && \
	apt-get install --yes \
		curl build-essential python \
		libcairo2-dev libgles2-mesa-dev \
		libgbm-dev libllvm3.9 libprotobuf-dev \
		libxxf86vm-dev libjpeg-dev xvfb \
		heat-cfntools software-properties-common
RUN curl --silent --location https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install --yes build-essential nodejs
