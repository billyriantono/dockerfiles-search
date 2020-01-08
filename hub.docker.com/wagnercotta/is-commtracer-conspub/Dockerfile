FROM python:3.6-slim

WORKDIR /opt/is-commtracer

COPY . .

RUN pip install -r requirements.txt

RUN rm -rf /usr/local/lib/python3.6/site-packages/opencensus \
    && cp -r opencensus /usr/local/lib/python3.6/site-packages

WORKDIR /opt/is-commtracer/src/conspub
