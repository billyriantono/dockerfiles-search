FROM node:9.6.1

RUN mkdir /usr/src/resume-siranee
WORKDIR /usr/src/resume-siranee

COPY package.json /usr/src/resume-siranee/
RUN npm install

COPY . /usr/src/resume-siranee

CMD ["npm","start"]

