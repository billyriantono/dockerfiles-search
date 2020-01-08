FROM ruby:2.4.2

MAINTAINER Kevin Wilson <kevin.wilson@dc.gov>

RUN apt-get update && \
    apt-get install -y build-essential \
                       libpq-dev \
                       libxml2-dev libxslt1-dev \
                       libqt4-webkit libqt4-dev xvfb \
		       vim \
                       python python-dev python-pip python-virtualenv && \
    rm -rf /var/lib/apt/lists/* && \
    cd /tmp && \
    wget http://nodejs.org/dist/v8.9.3/node-v8.9.3.tar.gz && \
    tar xvzf node-v8.9.3.tar.gz && \
    rm -f node-v8.9.3.tar.gz && \
    cd node-v* && \
    ./configure && \
    CXX="g++ -Wno-unused-local-typedefs" make && \
    CXX="g++ -Wno-unused-local-typedefs" make install && \
    cd /tmp && \
    rm -rf /tmp/node-v* && \
    npm install -g npm && \
    echo '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc && \
    gem install bundler

WORKDIR /app
ONBUILD ADD . /app

CMD ["bash"]
