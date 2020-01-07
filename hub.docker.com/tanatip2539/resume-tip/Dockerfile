FROM node:9.6.1

RUN mkdir /usr/src/myprofile
WORKDIR /usr/src/myprofile

COPY package.json /usr/src/myprofile/
RUN npm install

COPY . /usr/src/myprofile

CMD ["npm","start"]

