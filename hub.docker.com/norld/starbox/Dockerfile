FROM python:3.7

COPY ./requirements.txt /requirements.txt
WORKDIR /

RUN pip install --upgrade pip \
    && pip --no-cache-dir install -r requirements.txt