FROM terragontech/node:6.9


MAINTAINER Terragon Engineering Team <ike>

RUN cd /

RUN mkdir -p production/

WORKDIR /production

ADD package.json /production/package.json

ADD . /production/

RUN npm install && npm cache clean

EXPOSE 5000

CMD ["npm","start"]
