# Set the base image to Ubuntu
FROM    ubuntu

# Install Node.js and other dependencies
RUN apt-get update && \
    apt-get -y install curl && \
    curl -sL https://deb.nodesource.com/setup | sudo bash - && \
    apt-get -y install python build-essential nodejs

# By default, run npm from default ENTRYPOINT: /bin/sh -c npm start
CMD ["npm", "start"]
