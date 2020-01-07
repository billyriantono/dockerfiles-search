FROM node:latest
COPY . /home/node/JenkinsBot
RUN cd /home/node/JenkinsBot && npm install
EXPOSE 5600
CMD ["node", "/home/node/JenkinsBot/server.js"]
