FROM node:10

WORKDIR /code
COPY package.json /code/
RUN npm install

COPY . /code

ENTRYPOINT ["/code/bin/spritezero"]
