FROM shawnzhu/ruby

RUN apt-get update


#Update kernel
RUN apt-get install -y linux-image-generic-lts-trusty

# from http://stackoverflow.com/questions/13018626/
RUN apt-get install -y python-software-properties git curl socat wget sudo

# Need following for running phantomjs https://gist.github.com/julionc/7476620 
RUN apt-get install -y build-essential chrpath libssl-dev libxft-dev
RUN apt-get install -y libfreetype6 libfreetype6-dev
RUN apt-get install -y libfontconfig1 libfontconfig1-dev

# from https://github.com/dockerfile/nodejs/blob/master/Dockerfile
# Install Node.js
RUN \
  cd /tmp && \
  curl -O http://nodejs.org/dist/v0.12.4/node-v0.12.4.tar.gz && \
  tar xvzf node-v0.12.4.tar.gz && \
  rm -f node-v0.12.4.tar.gz && \
  cd node-v* && \
  ./configure && \
  CXX="g++ -Wno-unused-local-typedefs" make && \
  CXX="g++ -Wno-unused-local-typedefs" make install && \
  cd /tmp && \
  rm -rf /tmp/node-v* && \
  npm install -g npm && \
  echo -e '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc
