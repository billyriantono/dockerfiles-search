FROM node:7.10

RUN mkdir -p /opt/app-root/src
WORKDIR /opt/app-root/src

COPY package.json /opt/app-root/src
RUN npm install
COPY . /opt/app-root/src
RUN chmod -R 777 /opt/app-root/src
RUN npm run build

EXPOSE 8080

CMD [ "npm", "start" ]
