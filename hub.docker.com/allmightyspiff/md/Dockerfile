############################################################
# Dockerfile to run Cloudant webserver thing
# Based on Ubuntu Image
############################################################

# Set the base image to use to Ubuntu
FROM ubuntu

MAINTAINER Christopher Gallo
RUN apt-get update
RUN apt-get install -y nodejs npm git vim
RUN git clone https://github.com/allmightyspiff/md.git /usr/local/src/md
RUN cd /usr/local/src/md; npm install
RUN npm install mddoc express


WORKDIR /usr/local/src/md
#CMD ["bash", "/start-md"]
CMD ["nodejs", "/usr/local/src/md/app.js"]
#ENTRYPOINT nodejs
EXPOSE 3000
