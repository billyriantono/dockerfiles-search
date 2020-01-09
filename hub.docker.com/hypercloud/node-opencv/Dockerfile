# Known issue: node-opencv module is not compatible with opencv 3.0

FROM hypercloud/opencv:2.4
MAINTAINER Junxiang Wei <junxiang.wei@nodeunify.com>

ADD ./app /usr/src/app

WORKDIR /usr/src/app

RUN npm install

VOLUME /usr/src/app

CMD ["npm", "start"]

