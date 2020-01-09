FROM node:latest

RUN npm install -g dat

WORKDIR /app

COPY start.sh .

ENTRYPOINT [ "bash", "/app/start.sh" ]
