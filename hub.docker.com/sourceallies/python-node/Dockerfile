FROM python:2.7.12

RUN \
  cd /tmp && \
  wget http://nodejs.org/dist/v6.5.0/node-v6.5.0.tar.gz && \
  tar xvzf node-v6.5.0.tar.gz && \
  rm -f node-v6.5.0.tar.gz && \
  cd node-v* && \
  ./configure && \
  CXX="g++ -Wno-unused-local-typedefs" make && \
  CXX="g++ -Wno-unused-local-typedefs" make install && \
  cd /tmp && \
  rm -rf /tmp/node-v* && \
  npm install -g npm && \
  echo -e '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc

RUN /usr/local/bin/npm install -g bower gulp
RUN /usr/local/bin/pip install awscli
