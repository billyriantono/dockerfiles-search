FROM node:6

RUN npm install --global gulp

RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN mkdir /gulp

WORKDIR /gulp

CMD ["gulp"]