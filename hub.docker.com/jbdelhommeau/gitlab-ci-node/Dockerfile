FROM node:7-wheezy

MAINTAINER Jean-Baptiste Delhommeau "jeanbadel@gmail.com"

RUN npm install -g gulp grunt bower yarn
RUN npm cache clean
RUN npm config set cache-min 9999999

#Bower config
ENV CI true
RUN echo '{ "allow_root": true }' > /root/.bowerrc

CMD [ 'node' ]
