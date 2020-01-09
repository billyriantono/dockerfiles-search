FROM node:8.9.4-alpine

#install Node
RUN apk add --no-cache make gcc g++ python git
RUN npm config set loglevel error
RUN npm install --verbose dredd
RUN apk del make gcc g++ python
ENV PATH ${PATH}:/node_modules/.bin

#install PHP7
RUN apk add --no-cache php7 php7-json

#RUN dredd
CMD ["dredd"]