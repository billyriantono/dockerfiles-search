# Dockerfile

FROM node:latest
LABEL Bogdan Gherasim "gbogdan23a@yahoo.com"
WORKDIR /alia

COPY . .

RUN git clone https://4864b0d7854914162aaac3181d4e24acdda52ed0@github.com/bogdan23a/myguides.git /alia/resources/static/markdown

RUN npm install

ENV PORT=8080
EXPOSE $PORT

ENTRYPOINT ["node", "app.js"]