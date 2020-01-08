FROM nginx:latest

# Install all dependences
RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y --no-install-recommends \
		build-essential \
		curl \

# install node and npm
RUN curl -sSL --show-error https://deb.nodesource.com/setup_11.x | bash -
RUN apt-get install -y nodejs

WORKDIR  /usr/share/nginx/html
