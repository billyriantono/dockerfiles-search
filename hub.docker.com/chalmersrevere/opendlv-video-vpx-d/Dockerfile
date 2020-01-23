FROM node:6

RUN apt-get update && apt-get install -y

RUN apt-get install -y xvfb fonts-takao fonts-wqy-zenhei fonts-thai-tlwg

RUN npm install -g phantomjs

COPY package*.json ./

RUN npm install

COPY . ./

EXPOSE 8891

CMD ["node", "./bin/manet", "--host=0.0.0.0"]
