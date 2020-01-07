FROM python:3.5.3

MAINTAINER t-ziw@microsoft.com

WORKDIR /app/

COPY requirements.txt /app/
RUN pip install -r ./requirements.txt

COPY main.py /app/

#ENTRYPOINT /bin/bash

ENV ENVIRONMENT local

ENTRYPOINT python ./main.py


