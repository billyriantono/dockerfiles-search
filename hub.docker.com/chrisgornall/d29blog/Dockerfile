FROM node:0.10
ADD package.json /tmp/package.json
RUN cd /tmp && npm install

RUN mkdir -p /opt/app && cp -a /tmp/node_modules /opt/app/
 
# From here we load our application's code in, therefore the previous docker
# "layer" thats been cached will be used if possible
WORKDIR /opt/app
ADD . /opt/app
RUN npm install -g nodemon

EXPOSE 3000

CMD ["nodemon", "keystone.js"]
