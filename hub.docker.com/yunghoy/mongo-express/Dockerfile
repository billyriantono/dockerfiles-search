FROM mhart/alpine-node

MAINTAINER yunghoy AAAATTTT uci DDDDOOOOTTTT edu

EXPOSE 8081

WORKDIR app

RUN npm i mongo-express && npm cache clean

CMD ["node", "./node_modules/mongo-express/app.js"]
