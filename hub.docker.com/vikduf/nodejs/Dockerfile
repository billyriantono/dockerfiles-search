FROM node:boron
WORKDIR /node
RUN npm install -g bower
RUN echo deb http://ftp.uk.debian.org/debian jessie-backports main \
                  >>/etc/apt/sources.list
RUN apt-get update
RUN apt-get install ffmpeg -y
EXPOSE 8888
CMD [ "npm", "start" ]
