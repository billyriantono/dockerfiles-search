FROM ruby:2.2
MAINTAINER Andy Truong <thehongtt@gmail.com>

RUN curl -sL https://deb.nodesource.com/setup_4.x | bash - \
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/* \
    && npm install -g grunt-cli \
    && npm install -g grunt-cli \
    && npm install -g bower \
    && echo '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc \
    && gem install sass \
    && gem update --system \
    && gem install compass \
    && gem install guard-livereload;

VOLUME ["/app"]
WORKDIR /app

CMD ["bash"]
