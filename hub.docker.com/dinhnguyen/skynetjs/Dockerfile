FROM node:12.2.0

MAINTAINER DinhNguyen <dinhdanvu@gmail.com>

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install NPM
COPY package.json /usr/src/app/
RUN npm install

# Bundle app source
COPY . /usr/src/app


EXPOSE 8080 8081 8082

CMD ["npm","start"]