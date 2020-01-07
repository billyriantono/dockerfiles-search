FROM l4app/ubuntu:16.04
MAINTAINER andrzej.domanski@look4app.pl

RUN apt-get update

# Install Node.js ans pm2
RUN apt-get install -y \
  nodejs npm && \
  npm install pm2 gulp bower -g

RUN ln -s /usr/bin/nodejs /usr/bin/node


# Create appropriate directories
RUN mkdir -p /var/nodejs/configs /var/nodejs/apps
RUN touch /var/nodejs/apps/app.js

# Expose Node.js on port 3000
EXPOSE 3000

# Define default command
CMD pm2 --no-daemon
