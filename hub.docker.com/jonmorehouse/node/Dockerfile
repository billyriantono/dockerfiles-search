FROM jonmorehouse/ubuntu
MAINTAINER Jon Morehouse <morehousej09@gmail.com>

# set up repositories for node
RUN apt-get -y install software-properties-common
RUN add-apt-repository ppa:chris-lea/node.js
RUN apt-get -y update

# install node most recent stable as well as npm
RUN apt-get -y install nodejs
# symlink nodejs to node
RUN ln -sf `which nodejs` /usr/bin/node

# install coffeescript
RUN npm install -g coffee-script

