FROM revolutionsystems/python:3.8.0-wee-optimized-lto

RUN apt-get update && \
    apt-get install -y –no-install-recommends uwsgi uwsgi-plugin-python3 && \
    pip install django grpcio pillow protobuf && \
    rm -rf /var/lib/apt/lists/*
