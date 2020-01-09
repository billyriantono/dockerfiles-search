FROM node:10.5-slim

WORKDIR /cxloc
ENV NODE_ENV development

COPY package.json /cxloc/package.json

RUN npm install --production

COPY cli.js /cxloc
COPY server.js /cxloc
COPY app/ /cxloc/app/
COPY lib/ /cxloc/lib/
COPY public/ /cxloc/public/
COPY cxextensions.csv /cxloc

EXPOSE 8080

ENTRYPOINT ["node","cli.js"]
