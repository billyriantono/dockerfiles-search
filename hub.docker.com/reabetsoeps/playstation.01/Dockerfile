#Download base starefossen/ruby-node:2-8 which has node and rsync
FROM starefossen/ruby-node:2-8


# Update Software repository
RUN gem update --system && \
    gem install compass && \
    npm install grunt-cli && \
    npm install bower
