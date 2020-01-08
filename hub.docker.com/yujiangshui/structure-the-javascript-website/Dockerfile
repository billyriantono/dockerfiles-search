FROM node:8

WORKDIR /usr/src/app
COPY . .

RUN npm ci && npm run build

EXPOSE 8899
CMD [ "npm", "start" ]
