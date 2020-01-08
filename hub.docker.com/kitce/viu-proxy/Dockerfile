FROM node:alpine

WORKDIR /viu-proxy
COPY . /viu-proxy

RUN npm install && npm cache clean --force

EXPOSE 3000

CMD ["npm","start"]
