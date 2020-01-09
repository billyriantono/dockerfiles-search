FROM node:0.10.32

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app


RUN npm install -g bower
RUN npm install -g gulp

ADD package.json /usr/src/app/
RUN npm install

ADD bower.json /usr/src/app/
RUN bower install --allow-root

ADD . /usr/src/app
RUN gulp prepublish

CMD [ "npm", "start" ]
EXPOSE 9000
