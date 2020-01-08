FROM node

RUN mkdir -p /src
WORKDIR /src

ADD package.json /src/
RUN npm install
ADD . /src/

EXPOSE 3000
CMD npm start
