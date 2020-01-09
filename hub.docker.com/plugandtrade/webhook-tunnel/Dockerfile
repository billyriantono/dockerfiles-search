FROM node:10-alpine

WORKDIR /webhook-tunnel
COPY package.json .
COPY package-lock.json .
RUN npm install
COPY src ./src
COPY docker/entrypoint.sh .

ENV FORWARD_URL http://localhost:8080

ENTRYPOINT [ "./entrypoint.sh" ]
