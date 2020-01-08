FROM node:6

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY ./ /usr/src/app/
RUN npm install --production
RUN npm install --production serve
EXPOSE 8080
CMD /usr/src/app/node_modules/.bin/serve -p 8080
