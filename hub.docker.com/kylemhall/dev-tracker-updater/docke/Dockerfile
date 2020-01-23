FROM node:8.11.2
WORKDIR /app
ADD . /app
RUN npm install
EXPOSE 3000
ENTRYPOINT [ "npm", "start" ]