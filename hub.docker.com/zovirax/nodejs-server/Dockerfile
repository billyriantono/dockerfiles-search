FROM alpine

ARG APP_DIR=app
RUN mkdir -p ${APP_DIR}
#VOLUME ${APP_DIR} not supported by Heroku 
WORKDIR ${APP_DIR}
COPY . . 

RUN apk add --update nodejs npm \
	&& npm install

CMD ["npm", "start"]

#EXPOSE 3000 not supported by Heroku
