# Pull base image.
FROM alexisno/ubuntu-dev

ENV NODE_VERSION=4.2.2

# Install basic packages.
RUN apt-get update && apt-get -y install python-software-properties python g++ make &&\
    apt-get clean && rm -rf /var/lib/apt/lists/* &&\
    cd /opt &&\
    wget https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz &&\
    tar xvzf node-v${NODE_VERSION}-linux-x64.tar.gz &&\
    ln -s /opt/node-v${NODE_VERSION}-linux-x64/bin/node /usr/local/bin/node &&\
    ln -s /opt/node-v${NODE_VERSION}-linux-x64/bin/npm /usr/local/bin/npm

# Set ownership on /var/www
RUN mkdir -p /var/www && chown dev:dev /var/www

# Install npm packages globally with user dev
USER dev
RUN echo "prefix = ~/.node" >> ~/.npmrc &&\
    echo "export PATH=$PATH:/home/dev/.node/bin/" >> ~/.zshrc &&\
    npm install -g node-gyp forever yo bower grunt-cli gulp-cli node-inspector longjohn debug
ENV PATH $PATH:/home/dev/.node/bin/

WORKDIR /var/www

CMD ["node"]
