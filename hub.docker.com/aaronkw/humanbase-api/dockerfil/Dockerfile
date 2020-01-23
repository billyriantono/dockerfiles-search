FROM node:11-alpine

RUN npm install -g yapi-cli --registry https://registry.npm.taobao.org && \
    yapi plugin yapi-plugin-gitlab && \
    yapi plugin yapi-plugin-export-docx-data

ENTRYPOINT ["/bin/sh","-c", "yapi", "server"]