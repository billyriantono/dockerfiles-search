FROM node:latest

WORKDIR /opt/app
ADD . /opt/app

ENV SETUP_TABLES=true PORT=80 DATABASE_URL=http://dynamodb:8000
EXPOSE 80
RUN npm install

CMD ["node", "bin/www"]
