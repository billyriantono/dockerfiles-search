FROM node:4.8.0-alpine
MAINTAINER github.com/zaibon/

EXPOSE 2368

WORKDIR /app
ADD . /app
RUN npm install --production
RUN npm update

VOLUME /app/content/data/

ENTRYPOINT ["npm", "start"]
