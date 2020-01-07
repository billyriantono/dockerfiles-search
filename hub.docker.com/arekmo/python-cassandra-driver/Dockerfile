FROM python:3.5-jessie
RUN apt-get update && apt-get install libev4 libev-dev && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN pip install cassandra-driver==3.19.0
