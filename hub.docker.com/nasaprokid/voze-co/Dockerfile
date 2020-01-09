FROM node:8

WORKDIR /usr/app
COPY package.json .

RUN npm install --only=production
COPY . .
RUN npm run build

EXPOSE 80
CMD [ "npm", "start" ]
