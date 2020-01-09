# APIS

FROM node:8
RUN mkdir -p /usr/src/apis
WORKDIR /usr/src/apis
COPY package.json /usr/src/apis/
RUN npm install -g pm2
RUN npm install
COPY . /usr/src/apis
EXPOSE 3000
CMD [ "pm2" , "start", "server/server.js", "--no-daemon" ]

#ENV NODE_ENV=development
#ENV DATABASE=mongodb://mongodb:27017/playground
#ENV PORT=3001

#EXPOSE 3001

#CMD [ "nodemon", "-L", "src/index.js" ]


