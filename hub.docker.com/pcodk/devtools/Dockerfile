FROM node:12
MAINTAINER Jan-Erik Revsbech <jer@peytz.dk>

RUN node -v
RUN npm -v

# Install Bower & Grunt
RUN npm install -g bower grunt-cli && \
    echo '{ "allow_root": true }' > /root/.bowerrc

# Install Webpack 3
RUN npm install -g webpack@3

# Install ruby
RUN apt-get update && \
    apt-get -y install ruby-full

# Install compass
RUN gem update --system && \
    gem install compass

RUN mkdir -p /var/www/application

# Define working directory.
WORKDIR /var/www/application

# Define default command.
CMD ["bash"]
