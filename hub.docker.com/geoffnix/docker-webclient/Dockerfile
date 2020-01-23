#
# Node.js w/ Bower & Grunt & Image processing & Compass
#

# Pull base image.
FROM library/node

# Install libs
RUN apt-get update && apt-get install -y ruby ruby-dev graphicsmagick imagemagick && \
            apt-get clean && \
            rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Compass
RUN gem install --no-rdoc --no-ri sass -v 3.4.22
RUN gem install --no-rdoc --no-ri compass

# Install Bower & Grunt
RUN npm install -g bower grunt-cli && \
    echo '{ "allow_root": true }' > /root/.bowerrc

CMD ["bash"]
