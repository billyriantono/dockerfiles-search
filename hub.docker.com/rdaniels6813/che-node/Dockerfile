# Copyright (c) 2012-2016 Codenvy, S.A.
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v1.0
# which accompanies this distribution, and is available at
# http://www.eclipse.org/legal/epl-v10.html
# Contributors:
# Codenvy, S.A. - initial API and implementation
# rdaniels6813@gmail.com - Updated to version 6.5.0 and switched Yeoman out for Angular-CLI and Aurelia-CLI
FROM codenvy/ubuntu_jre

ENV NODE_VERSION 6.5.0
ENV NODE_PATH /usr/local/lib/node_modules

RUN sudo apt-get update && \
 sudo apt-get upgrade -y && \
 sudo apt-get install -y curl build-essential libssl-dev libkrb5-dev gcc make ruby-full rubygems-integration python unzip bash sudo git subversion && \
 sudo sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
RUN sudo gem install sass compass && \
    sudo apt-get clean && \
    sudo apt-get -y autoremove && \
    sudo apt-get -y clean && \
    sudo rm -rf /var/lib/apt/lists/* && \
    set -ex \
    && for key in \
  0xb63b535a4c206ca9 \
      9554F04D7259F04124DE6B476D5A82AC7E37093B \
      94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
      0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
      FD3A5288F042B6850C66B31F09FE44734EB7990E \
      71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
      DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    ; do \
      sudo gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
    done && \
  sudo mkdir -p /home/user && cd /home/user && sudo curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
  && sudo curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
  && sudo gpg --verify SHASUMS256.txt.asc \
  && sudo grep "node-v$NODE_VERSION-linux-x64.tar.gz\$" SHASUMS256.txt.asc | sha256sum -c - \
  && sudo tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
  && sudo rm "node-v$NODE_VERSION-linux-x64.tar.gz" SHASUMS256.txt.asc

RUN cd $(npm root -g)/npm \
  && sudo npm install fs-extra \
  && sudo sed -i -e s/graceful-fs/fs-extra/ -e s/fs\.rename/fs.move/ ./lib/utils/rename.js

RUN sudo npm install -g npm@latest
RUN sudo npm install -g typings gulp bower grunt grunt-cli angular-cli aurelia-cli yeoman-generator yo generator-angular generator-karma generator-webapp

EXPOSE 3000 3001 4200 5000 8080 9000

WORKDIR /projects

CMD tail -f /dev/null