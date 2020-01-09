FROM node:7.5-alpine
RUN npm set progress=false && \
    npm install -g --progress=false yarn && \
    apk add bash busybox --update
ENTRYPOINT bash
