FROM python:2.7-alpine
RUN apk add --update git python python-dev py-pip build-base postgresql-dev
RUN pip install virtualenv
RUN rm -rf /var/cache/apk/*
CMD /bin/sh
