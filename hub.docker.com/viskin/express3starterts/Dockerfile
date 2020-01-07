FROM node:4.2

MAINTAINER Roman Viskin <npm@terikon.com>

ENV PORT 8888
ENV APP /usr/src/app

#RUN apt-get -y update

# Create app directory
RUN mkdir -p $APP
WORKDIR $APP

# Application Code
COPY package.json $APP/
RUN npm install

COPY . $APP

# Start node
EXPOSE $PORT
CMD ["npm", "start"]
