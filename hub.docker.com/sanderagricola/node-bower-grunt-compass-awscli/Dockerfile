FROM node:10.15-slim

#Install stuff needed by the following steps
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils ruby ruby-dev gcc make libc6-dev unzip python-dev bzip2 git

#Install bower, grunt and compass
RUN npm install -g bower && npm install -g grunt && npm install phantomjs-prebuilt
RUN gem update --system && gem install compass && rm -rf /var/lib/apt/lists/*

#Re-install grunt-contrib-imagemin to fix permission issues
RUN npm uninstall grunt-contrib-imagemin && npm install grunt-contrib-imagemin

# Install awscli
RUN wget "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" \
    && unzip awscli-bundle.zip \
    && rm awscli-bundle.zip
RUN ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
RUN rm -rf awscli-bundle