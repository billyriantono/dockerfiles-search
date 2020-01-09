FROM node:alpine

RUN mkdir -p /app
WORKDIR /app

RUN npm config set registry https://registry.npmjs.org

#ToDo Remove for Production
RUN npm install -g nodemon
RUN npm install node-sass

RUN npm install express --save
RUN npm install pug --save
RUN npm install mysql2 --save
RUN npm install sequelize --save
RUN npm install body-parser --save

COPY package.json /app/package.json
RUN npm install \
 && npm ls \
 && npm cache clean --force \
 && mv node_modules /node_modules
COPY app /app

COPY startEnvironment.sh /startEnvironment.sh

ENV PORT 80
ENV MYSQL_HOST localhost
ENV MYSQL_PORT 3306
ENV MYSQL_USER root
ENV MYSQL_PASSWORD ""
ENV ENVIRONMENT PRODUCTION

EXPOSE 80

RUN /node_modules/node-sass/bin/node-sass /app/scss -o /app/public/

CMD ["sh", "/startEnvironment.sh"]