FROM node:7
RUN mkdir /node-postgres-docker
ADD . /node-postgres-docker
WORKDIR /node-postgres-docker
RUN npm i
EXPOSE 8080
CMD ["npm", "start"]
