FROM node:8.9.3

ENV ENV PAPERBOY_VERSION 0.5.1

RUN apt-get update -qq && \
    apt-get install -y -qq nginx supervisor && \
    apt-get clean -qq && \
    npm i -g @neoskop/paperboy-cli@$PAPERBOY_VERSION

COPY docker-entrypoint.sh /
COPY *.conf /home/node/
RUN mkdir /app && \
    chown -R node:node /app && \
    chown -R node:node /var/log/nginx
USER node
WORKDIR /app

EXPOSE 3000
VOLUME ["/data"]
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["paperboy start"]