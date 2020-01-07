FROM node:0.10.40

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY ./app/ ./
RUN npm install

EXPOSE 3000

CMD ["node", "app.js"]
