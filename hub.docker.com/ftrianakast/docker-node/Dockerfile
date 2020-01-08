# It builds an image with ubuntu 13.10 and nodejs

# use the ubuntu base image provided by dotCloud
FROM ubuntu:13.10
MAINTAINER Felipe Triana, ftrianakast@gmail.com

# make sure the package repository is up to date
RUN apt-get update

# install nodejs
RUN apt-get -y install software-properties-common python-software-properties python g++ make
RUN add-apt-repository ppa:chris-lea/node.js
RUN apt-get update
RUN apt-get -y install nodejs
RUN npm install -g nodemon

# expose the port
EXPOSE 8000

# adding start shell script
ADD start.sh /start.sh
RUN chmod +x /start.sh
WORKDIR /var/www

# init the application
CMD ["/start.sh"]