FROM node:10

RUN mkdir /myapp
WORKDIR /myapp
ADD package.json /myapp/package.json
ADD package-lock.json /myapp/package-lock.json
RUN npm install
ADD . /myapp