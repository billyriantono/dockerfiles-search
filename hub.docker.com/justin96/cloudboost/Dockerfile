FROM justin96/nodejs:latest

MAINTAINER Justin, justin.le.1105@gmail.com

ENV MONGO_HOST 3.0.207.184
ENV MONGO_PORT 27017
ENV REDIS_HOST 3.0.207.184
ENV REDIS_PORT 6379
ENV SMTP_PROVIDER sendgrid
ENV SMTP_APIKEY XXXXXXXXXXXXXXXXXXXXXXX
ENV SMTP_DOMAIN letuan.info
ENV SMTP_FROM_EMAIL contact@letuan.info
ENV SMTP_FROM_NAME Justin
ENV ELASTICSEARCH_HOST elasticsearch
ENV ELASTICSEARCH_PORT 9200

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

RUN git clone https://github.com/leanhtuan1996/cloudboost

WORKDIR /usr/src/app/cloudboost

RUN echo 'module.exports = { \n\
    "mongo": [{ \n\
        "host": "'${MONGO_HOST}'", \n\
        "port": "'${MONGO_PORT}'" \n\
    }], \n\
    "elasticsearch": [{ \n\
        "host": "elasticsearch", \n\
        "port": "9200" \n\
    }], \n\
    "redis": [{ \n\
        "host": "'${REDIS_HOST}'", \n\
        "port": "'${REDIS_PORT}'" \n\
    }] \n\
}' > ./config/cloudboost.js

RUN echo 'module.exports = { \n\
  "provider"  : "'${SMTP_PROVIDER}'", \n\
  "apiKey"    : "'${SMTP_APIKEY}'", \n\
  "domain"    : "'${SMTP_DOMAIN}'", \n\
  "fromEmail" : "'${SMTP_FROM_EMAIL}'", \n\
  "fromName"  : "'${SMTP_FROM_NAME}'" \n\
}' > ./config/smtp.js

RUN npm install

EXPOSE 4730

CMD [ "node", "server.js" ]
