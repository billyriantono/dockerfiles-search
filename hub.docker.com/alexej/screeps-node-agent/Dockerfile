FROM node:9
WORKDIR /app
ENV AGENT_CONFIG_PATH /config/config.js
ENV DOCKER true
ADD package.json /app
RUN yarn install
ADD app.js .
CMD ["yarn","start"]
