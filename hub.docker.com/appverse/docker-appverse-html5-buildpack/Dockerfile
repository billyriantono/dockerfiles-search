FROM node:6-slim

RUN apt-get update && apt-get install -y \
    bzip2 \
    git \
    openjdk-7-jre \
    && rm -rf /var/lib/apt/lists/*

RUN git config --global url."https://github.com/".insteadOf "git://github.com/" && \
    echo '{ "allow_root": true }' > ~/.bowerrc

RUN npm install -g bower grunt-cli

RUN npm install -g phantomjs-prebuilt@^2.1.12
RUN npm uninstall -g phantomjs-prebuilt

RUN npm install -g node-sass
ENV SASS_BINARY_PATH /usr/local/lib/node_modules/node-sass/vendor/linux-x64-48/binding.node

CMD ["bash"]
