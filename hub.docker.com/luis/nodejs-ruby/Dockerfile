FROM ubuntu:14.04
MAINTAINER Luis Elizondo "lelizondo@gmail.com"

ENV DEBIAN_FRONTEND noninteractive

# Update
RUN apt-get update && apt-get dist-upgrade -y
RUN apt-get update --fix-missing

# Install everything needed
RUN apt-get install -y nodejs npm git ruby
RUN apt-get install -y supervisor

# Link nodejs to avoid problems
RUN ln -s /usr/bin/nodejs /usr/local/bin/node

# Install global node packages and compass
RUN npm install -g express bower grunt yo pg grunt-cli
RUN apt-get install -y ruby-dev
RUN gem update
RUN gem install compass
RUN npm install -g karma
RUN apt-get install -y xdg-utils
RUN apt-get update --fix-missing

# Cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN apt-get autoremove -y

# Ensure UTF-8
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# Create supervisor log directory
RUN mkdir -p /var/log/supervisor

# Add supervisor file
ADD ./config/supervisord.conf /etc/supervisor/conf.d/supervisord-nodejs.conf


# Expose the ports
EXPOSE 3000
EXPOSE 9000
EXPOSE 9001

# Set NODE_ENV as development by default
ENV NODE_ENV development

WORKDIR /var/www

VOLUME ["/var/www"]

CMD ["/usr/bin/supervisord", "-n"]
