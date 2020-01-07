FROM node:5-slim

RUN npm install -g easymock

VOLUME ["/data"]

WORKDIR /data

EXPOSE 3000

ENTRYPOINT ["easymock", "-p", "3000"]
