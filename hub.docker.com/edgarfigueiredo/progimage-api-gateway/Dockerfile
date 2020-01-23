FROM node:12.13-alpine
LABEL Author=edgar@edgarneto.com
ADD . /app
WORKDIR /app
RUN npm install
EXPOSE 3000
ENTRYPOINT [ "node", "index.js" ]