FROM node:8

COPY package-lock.json package.json ./
RUN npm install

COPY . .

RUN npm run build

CMD ["npm", "run", "start"]