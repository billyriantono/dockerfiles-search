FROM node:13

# install server dependencies
ADD server/package.json /server/package.json
RUN cd /server && NODE_ENV=production npm install

# install client dependencies
ADD client/app/package.json /client/app/package.json
RUN cd client/app && npm install

# add client sources and build client
ADD client/ /client
RUN cd /client/app && npm run build

# add server sources
ADD server/ /server

CMD cd /server && npm start

EXPOSE 3000
