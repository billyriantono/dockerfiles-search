FROM node:10

ENV NODE_ENV development

WORKDIR /usr/app

COPY package.json .

RUN npm install	#kazdy run tworzy nowa warstwe

COPY src ./src

COPY public ./public

CMD ["npm","start" ]
