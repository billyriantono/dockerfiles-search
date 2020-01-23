FROM node:latest

#Create Working Directory
RUN mkdir -p /usr/src/bot
WORKDIR /user/src/bot

#Copy and Install the bot
COPY package.json /usr/src/bot
RUN npm install

COPY . /usr/src/bot

CMD ["node","bot.js"]


