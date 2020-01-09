# Set the base image to Debian Jessie with Nodesource Node.js binaries
FROM nodesource/jessie:0.10

MAINTAINER Chris Hedgate

RUN ["npm", "i", "pm2", "-g"]
RUN ["npm", "i", "nodemon", "-g"]

CMD ["/bin/bash"]