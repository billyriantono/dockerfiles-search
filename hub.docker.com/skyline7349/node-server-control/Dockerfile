FROM node:jessie
RUN apt-get update && apt-get install -y wakeonlan
WORKDIR /app
COPY package.json .
RUN npm install --global bower
RUN npm install --production
COPY . .
RUN bower install --quiet --allow-root --config.interactive=false
ENV PORT=8080
EXPOSE ${PORT}
CMD npm run start
