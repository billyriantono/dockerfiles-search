FROM node:5.10.1


RUN apt-get update && apt-get install yamdi -y

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD COPY package.json /usr/src/app/
ONBUILD COPY . /usr/src/app

CMD [ "npm", "start" ]
