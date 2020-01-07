FROM node:6.14.3

MAINTAINER contact@ramandeep.com

#Copy code to /app
COPY . /app

WORKDIR /app

#Install app and dependencies into /app
RUN npm install \
    && npm install --global mocha \
    && npm install forever -g
#RUN npm start

EXPOSE 8088

CMD ["node","./app.js"]