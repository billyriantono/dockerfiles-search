FROM node:10-alpine

COPY package*.json ./
RUN npm install
COPY *.js ./

CMD ["npm", "start"]
