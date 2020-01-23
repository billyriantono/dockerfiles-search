FROM ezekov/node-nginx:latest

COPY . .

ENV PORT=${PORT}

RUN sh ./scripts/install.sh

CMD [ "sh", "./scripts/run.sh" ]