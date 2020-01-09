FROM node:9.6.1

RUN mkdir /usr/src/resume
WORKDIR /usr/src/resume

COPY package.json /usr/src/resume/
RUN npm install

COPY . /usr/src/resume

CMD ["npm","start"]

