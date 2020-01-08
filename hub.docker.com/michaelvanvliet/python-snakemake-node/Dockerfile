FROM python:3.7.3-slim-stretch

LABEL maintainer="m.s.vanvliet@lacdr.leidenuniv.nl"

COPY requirements.txt /tmp/

# runtime dependencies list
RUN apt-get update && \ 
    apt-get install -y --no-install-recommends unzip wget && \
    rm -rf /var/lib/apt/lists/* && \
    pip install -r /tmp/requirements.txt

CMD ["python3"]    