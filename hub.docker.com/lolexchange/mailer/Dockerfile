FROM node

RUN apt-get update && apt-get install -y \
	build-essential \
	python

WORKDIR /usr/src/app
RUN npm i nodemon -g

COPY package.json ./

RUN npm install --production
RUN npm rebuild bcrypt
COPY . .

CMD ["node", "index.js"]
