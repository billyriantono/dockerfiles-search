FROM node:6.10.0-slim

ENV INSTALL_DIR /dashboard

# Install Ubuntu dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
		git \
        wget \
        tar \
        bzip2 \
        graphicsmagick \
        libfontconfig

# Copy project files
RUN mkdir $INSTALL_DIR
WORKDIR $INSTALL_DIR
ADD . $INSTALL_DIR

# Install yarn and bower dependencies
RUN \
	yarn global add bower ember-cli@2.12.0 phantomjs-prebuilt &&\
	yarn install --force &&\
	bower install --allow-root

EXPOSE 4200 49153

CMD ["yarn", "run", "start"]
