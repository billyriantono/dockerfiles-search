FROM node:10

RUN mkdir -p /usr/src/app

ADD . /usr/src/app
WORKDIR /usr/src/app

RUN npm i
RUN git clone https://github.com/vishnubob/wait-for-it.git

EXPOSE 3000
CMD ["npm", "start"]
