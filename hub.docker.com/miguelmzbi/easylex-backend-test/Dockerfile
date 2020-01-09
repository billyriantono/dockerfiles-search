FROM node:11
LABEL maintainer Miguel Montoya <miguel.mzbi@gmail.com>

RUN mkdir /easylex_backend_test
ADD . /easylex_backend_test/
WORKDIR /easylex_backend_test
RUN npm install
EXPOSE 1337
CMD ["npm", "start"]