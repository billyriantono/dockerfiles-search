# określamy z jakiego obrazu dockera będziemy budować swój własny
FROM node:10-alpine

# usatwienie zmiennej środowiskowej
ENV NODE_ENV development

# katalog, w którym będziemy po uruchomieniu kontenera
WORKDIR /usr/app

COPY package.json .

RUN npm install

# kopiowanie folderu do obraza, ktrory bedziemy budować
COPY src src

COPY public public

CMD ["npm", "start"]
