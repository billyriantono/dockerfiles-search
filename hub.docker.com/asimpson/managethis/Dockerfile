FROM alpine
MAINTAINER Adam Simpson <simpsonadam@gmail.com>

RUN apk add --update nodejs
RUN apk update && apk upgrade
RUN rm -rf /var/cache/apk/*

WORKDIR /opt
COPY ./ /opt
RUN cp config.json.template config.json
RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
