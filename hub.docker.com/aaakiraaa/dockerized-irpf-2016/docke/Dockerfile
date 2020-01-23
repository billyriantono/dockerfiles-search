FROM ruby:2.3.0
MAINTAINER Felipe Benevides <felipe.benevides@99taxis.com>

# node dependencies
RUN apt-get update -qq && apt-get install -y build-essential
RUN apt-get install -y python python-dev python-pip python-virtualenv
RUN rm -rf /var/lib/apt/lists/*

# node stuff
RUN \
  cd /tmp && \
  wget http://nodejs.org/dist/node-latest.tar.gz && \
  tar xvzf node-latest.tar.gz && \
  rm -f node-latest.tar.gz && \
  cd node-v* && \
  ./configure && \
  CXX="g++ -Wno-unused-local-typedefs" make && \
  CXX="g++ -Wno-unused-local-typedefs" make install && \
  cd /tmp && \
  rm -rf /tmp/node-v* && \
  npm install -g npm && \
  npm install cult && \
  echo '{ "allow_root": true }' > /root/.bowerrc && \
  echo '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc

CMD ["bash"]
