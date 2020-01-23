FROM node:4
# ENV http_proxy=http://16.85.88.10:8080 https_proxy=http://16.85.88.10:8080
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ARG NODE_ENV
ENV NODE_ENV $NODE_ENV
EXPOSE 3000
RUN npm config set strict-ssl false
COPY package.json /usr/src/app
RUN npm install && npm cache clean
COPY . /usr/src/app

CMD ["npm", "start"]
