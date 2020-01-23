FROM python:3.7-alpine

LABEL maintainer "Yefta Sutanto <yefta@bitwyre.com>"

COPY --from=bitwyre/base-images:python-alpine /app/bitwyre/base-python/wheels /app/bitwyre/uds/wheels

COPY ./requirements.txt /app/bitwyre/uds/requirements.txt

WORKDIR /app/bitwyre/uds

RUN pip install --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt \
                -f /app/bitwyre/uds/wheels && \
    rm -rf /app/bitwyre/uds/wheels && \
    rm -rf /root/.cache/pip/*

RUN apk --no-cache add bash

COPY ./run.sh /app/bitwyre/uds/run.sh
COPY ./README.md /app/bitwyre/uds/README.md
COPY ./setup.py /app/bitwyre/uds/setup.py
COPY ./bitwyre_uds /app/bitwyre/uds/bitwyre_uds

RUN python setup.py install
RUN chmod +x ./run.sh

EXPOSE 3003

ENTRYPOINT ./run.sh
