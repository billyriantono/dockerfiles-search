FROM node:12-alpine
#FROM keymetrics/pm2

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

#RUN ls

COPY package.json /usr/src/app
#COPY ./ /usr/src/app
#ADD . /usr/src/app

COPY . /usr/src/app
#RUN npm install pm2 -g
RUN npm install


EXPOSE 3011

CMD ["npm", "run", "start:prod"]
#COPY ecosystem.config.js .
#ENTRYPOINT [ "pm2-runtime" ]
#CMD [ "start", "ecosystem.config.js" ]