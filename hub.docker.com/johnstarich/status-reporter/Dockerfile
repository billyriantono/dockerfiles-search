FROM node:10-alpine

COPY package-lock.json package.json /
RUN npm install
COPY . /
CMD ["node", "app.js"]
