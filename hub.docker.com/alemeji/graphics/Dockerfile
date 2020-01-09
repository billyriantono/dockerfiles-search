FROM python:2.7.15-slim-stretch as base

FROM base as builder

ENV PYTHONDONTWRITEBYTECODE=1
ENV DJANGO_ENV=local

RUN apt-get update && apt-get install -y --no-install-recommends \
		build-essential \
        default-libmysqlclient-dev \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /wheels
COPY graphics/requirements/ /wheels/requirements/
RUN pip install -U pip && pip wheel -r ./requirements/$DJANGO_ENV.txt

FROM base

LABEL maintainer="alemeji@gmail.com"

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV DJANGO_ENV=local

ENV WEBAPP_DIR=/webapp
ENV PISA=/usr/local/lib/python2.7/site-packages/sx/pisa3

RUN apt-get update && apt-get install -y --no-install-recommends \
        # build-essential \
        default-libmysqlclient-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir $WEBAPP_DIR

WORKDIR $WEBAPP_DIR

COPY --from=builder /wheels /wheels

RUN pip install -U pip \
    && pip install -r /wheels/requirements/$DJANGO_ENV.txt -f /wheels \
    && rm -rf /wheels \
    && rm -rf /root/.cache

ADD . $WEBAPP_DIR/
ADD pisa_util.py $PISA/

EXPOSE 8000

