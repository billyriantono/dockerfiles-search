FROM node:alpine

RUN mkdir -p /usr/src/scraper
WORKDIR /usr/src/scraper

COPY . /usr/src/scraper/
RUN npm install

RUN npm run build

EXPOSE 3000

ENV NUXT_HOST=0.0.0.0

CMD [ "npm", "start" ]