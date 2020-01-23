FROM node:0.12

RUN npm install -g dredd

ENV API_ENDPOINT=http://localhost:8080
ENV MD_PATH=./apiary.md

RUN mkdir -p /usr/src/dredd
WORKDIR /usr/src/dredd

CMD dredd $MD_PATH $API_ENDPOINT
