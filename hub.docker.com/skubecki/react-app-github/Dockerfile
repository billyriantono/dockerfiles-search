FROM node:10-alpine

#zmienna srodowiskowa
ENV NODE_ENV development

WORKDIR /usr/app

COPY package.json .

#zainstaluj rzeczy node'owe z pliku json
RUN npm install

COPY src src

COPY public public

#co ma zostac wywolane po uruchomieniu kontenera
CMD ["npm","start"]
