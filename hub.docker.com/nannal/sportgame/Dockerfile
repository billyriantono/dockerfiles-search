FROM node:10-alpine
LABEL "project.home"="https://github.com/nannal/sportgame"
COPY ./ /sportgame
WORKDIR /sportgame
RUN npm install

ENV DiscordID 'FalseValue'
ENV DB_URL 'mongodb://localhost:27017'
ENV DB_NAME 'sportgame'
CMD ["node","index.js"]
