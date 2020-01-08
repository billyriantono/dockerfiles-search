FROM node:alpine

COPY . /application/
RUN cd /application/ && \
    npm install

ENTRYPOINT ["node", "/application/index.js"]
EXPOSE 9200
