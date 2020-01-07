FROM node:6.14.3-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
  && rm -rf /var/lib/apt/lists/*

RUN npm install -g bower grunt-cli gulp-cli yarn

RUN echo '{ "allow_root": true }' > /root/.bowerrc

################################################################################
# Working directory
################################################################################
WORKDIR /app/src

RUN mkdir /.npm\
	&& chmod -R 777 /.npm
RUN mkdir /.config\
	&& chmod -R 777 /.config
RUN mkdir /.cache\
	&& chmod -R 777 /.cache
RUN mkdir /.local\
	&& chmod -R 777 /.local

################################################################################
# Volumes; allow the /app/src directory to be mounted by the host
################################################################################
VOLUME ["/app/src"]
