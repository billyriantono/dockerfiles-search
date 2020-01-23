FROM node:6.11.3
# replace this with your application's default port

RUN npm install express-generator -g
RUN npm install nodemon -g
RUN npm install -g typescript

WORKDIR /usr/src/app


EXPOSE 3000
EXPOSE 5858

#CMD ["nodemon", "-L", "/usr/src/app/bin/www"]