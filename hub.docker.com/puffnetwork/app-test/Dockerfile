FROM node:8.15.1-alpine
ENV HOST 0.0.0.0

RUN mkdir -p /app

EXPOSE 8080

COPY . /app
WORKDIR /app
RUN npm install
RUN npm run build

CMD [ "npm", "start" ]
