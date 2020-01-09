from node:alpine

WORKDIR /app
ENV PORT 3001
ENV IMAGES_BASEDIR=/data
COPY ./src /app/
RUN cd /app/webapp \
    && npm install \
    && npm run build \
    && mv build ../server/ \
    && npm prune --production \
    && cd /app/server \
    && npm install \
    && rm -rf /app/webapp

EXPOSE 3001
WORKDIR /app/server
CMD npm start
