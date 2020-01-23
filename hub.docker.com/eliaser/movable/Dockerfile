FROM node:alpine
COPY ui/package.json ./app/
WORKDIR app
RUN npm install
COPY ui .
EXPOSE 3000
CMD [ "npm", "start" ]