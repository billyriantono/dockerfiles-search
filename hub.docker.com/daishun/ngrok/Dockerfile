FROM node:8.12-alpine

RUN mkdir app
COPY ./ /app
EXPOSE 4040
WORKDIR /app
RUN npm install ngrok --registry=https://registry.npm.taobao.org --save
CMD ["npm","start"]