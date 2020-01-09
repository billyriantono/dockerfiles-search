FROM node:11.15.0-alpine

WORKDIR /code

COPY package.json .
COPY package-lock.json .
RUN npm install

COPY public/ public/
COPY routes/ routes/
COPY views/ views/
COPY index.js .

EXPOSE 3000

CMD ["npm", "start"]
