FROM node:10-alpine
WORKDIR /usr/src/app
COPY app .
RUN npm install
EXPOSE 8080
USER 1001
CMD [ "npm", "start" ]
