FROM node:10.13

WORKDIR bytes-frontend
COPY package*.json ./

RUN npm install
COPY . .

RUN npm run build
CMD [ "npm", "start" ]