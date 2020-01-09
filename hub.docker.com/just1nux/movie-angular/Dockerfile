FROM node:11.7

WORKDIR /usr/src/app

ENV PATH /usr/src/app/node_modules/.bin:$PATH

COPY package*.json /usr/src/app/

RUN npm install

COPY . /usr/src/app
ARG configuration=production

RUN npm run build -- --output-path=./dist/out --configuration 

CMD cp -r /usr/src/app/dist/out/* /usr/share/nginx/html