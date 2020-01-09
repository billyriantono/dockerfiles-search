FROM node:8
WORKDIR /usr/src/app
COPY package*.json ./

RUN npm install
RUN npm install pm2 -g && pm2 update

COPY . .

EXPOSE 3000

CMD ["pm2-runtime","start", ".", "--name", "lbexp"]