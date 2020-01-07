FROM ubuntu
MAINTAINER Aaron <aronanda@gmail.com>

# Install Node.js and other dependencies
RUN apt-get update
RUN apt-get -y install curl
RUN curl -sL https://deb.nodesource.com/setup | sudo bash -
RUN apt-get -y install python build-essential nodejs
# RUN apt-get install -y nodejs nodejs-legacy npm
# RUN apt-get clean

# Install latest npm
RUN npm install -g npm@latest

# Install nodemon
RUN npm install -g nodemon

COPY ./package.json src/

RUN cd src && npm install

COPY . /src

WORKDIR src/

# Expose port
EXPOSE  8080

# Run app using nodemon
CMD ["nodemon", "/src/server.js"]
