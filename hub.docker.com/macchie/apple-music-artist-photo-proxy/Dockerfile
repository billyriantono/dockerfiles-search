FROM node:10

WORKDIR /app

COPY ./package*.json /app/

RUN npm install -g typescript

RUN npm install

COPY ./ ./

RUN npm run build

EXPOSE 5000

CMD ["npm", "start"]