FROM node:8
# RUN apk update && apk upgrade && apk add --no-cache \
#     curl bash
# RUN curl "https://install.meteor.com/" | /bin/sh
# RUN useradd meteor -G staff -m -s /bin/bash
RUN curl https://install.meteor.com/ > meteor.sh \
    && chmod 777 ./meteor.sh \ 
    && ./meteor.sh
RUN npm i -g mupx
ENV METEOR_ALLOW_SUPERUSER=true
USER meteor
EXPOSE 3000
