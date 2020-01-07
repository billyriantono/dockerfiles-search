FROM node:12
WORKDIR /nodeapp
COPY package.json /nodeapp
RUN npm install
COPY . /nodeapp
CMD node app.js
EXPOSE 80