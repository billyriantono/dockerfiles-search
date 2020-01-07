FROM python:alpine

RUN apk add --no-cache bash git  \
        && pip install --upgrade pip \
        && pip install flask \
        && pip install flasgger \
        && pip install pika

# application folder
ENV APP_DIR /app

# expose web server port
EXPOSE 5000

# copy the application and theentry point
COPY entrypoint.sh /entrypoint.sh

# exectute start up script
ENTRYPOINT ["/entrypoint.sh"]

