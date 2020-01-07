FROM node:latest
RUN mkdir -p /home/node/jenkinsbot
WORKDIR /home/node/jenkinsbot
COPY package.json /home/node/jenkinsbot/
RUN npm install
COPY . /home/node/jenkinsbot
EXPOSE 4444
CMD ["npm", "start"]