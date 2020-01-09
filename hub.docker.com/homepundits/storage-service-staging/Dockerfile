FROM homepundits/node:6.9.1

MAINTAINER Home Pundits Engineering Team <oseme.odigie@gmail.com>

RUN cd /

RUN mkdir -p production/app

RUN mkdir -p production/app/logs

WORKDIR /production

ADD package.json /production/package.json

# ADD package-lock.json /production/package-lock.json

ADD app /production/app

RUN npm install && npm cache clean

EXPOSE 9892

CMD npm start