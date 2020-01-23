FROM python:3.6.6-alpine

RUN pip install --upgrade hvac==0.5.0 && \
    mkdir -p /usr/src/app/drone-vault

ENV PYTHONPATH /usr/src/app
WORKDIR /usr/src/app/drone-vault

COPY run.py /usr/src/app/drone-vault/
CMD python /usr/src/app/drone-vault/run.py