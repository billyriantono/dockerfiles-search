FROM node:carbon

COPY package.json ./
RUN yarn

COPY . ./
RUN yarn webpack

EXPOSE 3000

CMD ["node", "server/index.js"]