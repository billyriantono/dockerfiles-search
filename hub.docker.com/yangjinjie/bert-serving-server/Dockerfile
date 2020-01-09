FROM tensorflow/tensorflow:1.14.0-gpu-py3

RUN apt-get update \
    && apt-get install wget \
    && apt-get autoclean && apt-get clean \
    && mkdir /app && cd /app \
    && wget https://storage.googleapis.com/bert_models/2018_11_03/chinese_L-12_H-768_A-12.zip \
    && unzip chinese_L-12_H-768_A-12.zip \
    && rm -f chinese_L-12_H-768_A-12.zip \
    && pip install bert-serving-server \
    && pip install -U bert-serving-server[http] \
    && rm -rf /root/.cache

WORKDIR /app

COPY ./docker/entrypoint.sh /app
ENTRYPOINT ["/app/entrypoint.sh"]
