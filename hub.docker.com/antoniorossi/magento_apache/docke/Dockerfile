FROM node:11.12.0

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN curl -sf -o /tmp/sonata.tar.gz -L https://github.com/antirek/sonata/archive/19.3.1.tar.gz && \
    tar -zxf /tmp/sonata.tar.gz -C /usr/src/app --strip-components=1

RUN npm install

COPY . /usr/src/app

CMD [ "npm", "start" ]
