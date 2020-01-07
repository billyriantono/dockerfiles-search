FROM node:lts-slim

RUN yarn global add serve

COPY entrypoint.sh /app/entrypoint.sh

RUN chmod +x /app/entrypoint.sh

VOLUME /serve

EXPOSE 5000

ENTRYPOINT ["/app/entrypoint.sh"]
