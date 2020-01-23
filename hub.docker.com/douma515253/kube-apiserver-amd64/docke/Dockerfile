FROM node
LABEL MAINTAINER dotty.skariya@gmail.com
run mkdir /code-app
add node.js /code-app/node.js
add data.json /code-app/data.json
RUN npm install -y express
RUN npm install -y body-parser
EXPOSE 9000
CMD node /code-app/node.js
