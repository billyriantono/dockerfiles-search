FROM node:lts-alpine
RUN yarn global add http-server
WORKDIR /app
COPY package*.json ./
COPY yarn.lock ./
RUN yarn install
COPY . .
RUN yarn run build
EXPOSE 8080
CMD [ "http-server", "dist" ]
