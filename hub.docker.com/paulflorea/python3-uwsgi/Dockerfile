FROM python:3.6-alpine

# Add necessary build-packages
RUN apk update; apk add gcc g++ make libffi-dev openssl-dev linux-headers

# So simple now
RUN pip install uwsgi