# Use ubuntu base docker image
FROM phusion/baseimage:latest
CMD ["/sbin/my_init"]

# Install updates and dependencies
RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates libkrb5-dev && \
    apt-get clean && rm /var/lib/apt/lists/*_*

# media
RUN add-apt-repository ppa:mc3man/trusty-media -y
RUN apt-get update
RUN apt-get -y dist-upgrade
RUN apt-get install -y ffmpeg imagemagick

# Install the latest LTS release of nodejs
RUN mkdir /nodejs && curl https://nodejs.org/dist/v4.2.4/node-v4.2.4-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ENV PATH $PATH:/nodejs/bin

# Timezone
ENV TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install semver, as required by the node version install script.
RUN npm install https://storage.googleapis.com/gae_node_packages/semver.tar.gz

# Add the node version install script
ADD install_node /usr/local/bin/install_node

# start
CMD ["npm", "start"]
