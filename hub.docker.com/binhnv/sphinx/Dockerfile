FROM binhnv/base
MAINTAINER "Binh Van Nguyen<binhnv80@gmail.com>"

ADD ./requirements.txt /tmp/requirements.txt
RUN apt-get update \
    && apt-get install make \
    && pip install -r /tmp/requirements.txt \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
