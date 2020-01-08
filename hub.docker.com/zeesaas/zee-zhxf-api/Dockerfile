FROM mhart/alpine-node:latest

WORKDIR /
COPY package.json /package.json
RUN npm i --registry=https://registry.npm.taobao.org

COPY src /src
COPY development.js /development.js
COPY production.js /production.js

# systemType
ENV SYSTEM_TYPE setYourValue
# config
ENV CONFIG_DEV_OSS_URL setYourValue
ENV CONFIG_DEV_OSS_STYLE setYourValue
ENV CONFIG_DEV_OSS_REGION setYourValue
ENV CONFIG_DEV_OSS_INTERNAL_REGION setYourValue
ENV CONFIG_DEV_OSS_KEY setYourValue
ENV CONFIG_DEV_OSS_SECRET setYourValue
ENV CONFIG_DEV_OSS_BUCKER setYourValue
ENV CONFIG_DEV_OSS_FOLDER_IMAGE setYourValue
ENV CONFIG_DEV_OSS_FOLDER_FILE setYourValue
# task
ENV CONFIG_TASK_INTERVAL setYourValue
ENV CONFIG_TASK_IMMEDIATE setYourValue
# pgsql-dev
ENV PGSQL_DEV_HOST setYourValue
ENV PGSQL_DEV_PORT setYourValue
ENV PGSQL_DEV_USER setYourValue
ENV PGSQL_DEV_PASSWORD setYourValue
ENV PGSQL_DEV_DATABASE setYourValue
ENV PGSQL_DEV_PREFIX setYourValue
# pgsql-pro
ENV PGSQL_PRO_HOST setYourValue
ENV PGSQL_PRO_PORT setYourValue
ENV PGSQL_PRO_USER setYourValue
ENV PGSQL_PRO_PASSWORD setYourValue
ENV PGSQL_PRO_DATABASE setYourValue
ENV PGSQL_PRO_PREFIX setYourValue
# baiduface
ENV BAIDU_FACE_ID setYourValue
ENV BAIDU_FACE_KEY setYourValue
ENV BAIDU_FACE_SECRET setYourValue
ENV BAIDU_FACE_BUCKET setYourValue
# device
ENV IOT_DEVICE_PORT setYourValue

ENV DOCKER=true
EXPOSE 18000

# CMD [ "node", "/production.js" ]
