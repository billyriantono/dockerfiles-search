FROM node:argon-slim

RUN apt-get update
RUN npm install -g notify-cli

COPY ./entry.sh /tmp
RUN chmod +x /tmp/entry.sh
ENTRYPOINT ["/tmp/entry.sh"]
