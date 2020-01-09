FROM sandinh/sbt-node

RUN curl -L https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 | \
        tar -jx -O phantomjs-2.1.1-linux-x86_64/bin/phantomjs | \
        sudo tee /usr/local/bin/phantomjs > /dev/null && \
      sudo chmod +x /usr/local/bin/phantomjs

RUN sudo mkdir /builds && sudo chown sandinh:sandinh /builds
