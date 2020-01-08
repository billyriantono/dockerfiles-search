FROM ubuntu:15.10

RUN apt-get update && \
    apt-get install -y ruby ruby-dev nodejs npm gcc git rsync make && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN gem install jekyll && \
    npm install gulp gulpfile-install -g