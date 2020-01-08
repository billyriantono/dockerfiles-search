FROM python:slim

RUN pip install --upgrade --no-cache-dir awsebcli
RUN apt-get -yqq update && apt-get -yqq install git-all

WORKDIR /home

ENTRYPOINT ["eb"]
