FROM node:8-alpine

WORKDIR /polly

COPY gulp /polly/gulp
COPY sample /polly/sample
COPY src /polly/src
COPY .babelrc .editorconfig gulpfile.babel.js package.json /polly/

EXPOSE 9000
EXPOSE 3001

RUN npm install
CMD npm run dev