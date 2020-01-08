FROM node
MAINTAINER Perlan Cloud <perlancloud@gmail.com>

# Bundle app source
ADD . /src

# Install app dependencies
RUN cd /src; npm install

# Expose Port 8080 and run Node.js application
EXPOSE  8080
CMD ["node", "/src/index.js"]
