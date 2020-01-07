FROM node:boron
# Create app directory

RUN mkdir -p /usr/src/myNode/app
WORKDIR /usr/src/myNode/app

# Install app dependencies
COPY package.json /usr/src/myNode/app/
RUN npm install

# Bundle app source
COPY . /usr/src/myNode/app

EXPOSE 3000
CMD ["node","app.js"]
