FROM ubuntu:18.04

RUN apt-get update && \
    apt-get install -y \
    python3 \
    python3-pip \
    python3-mysql.connector && \
    apt-get clean

WORKDIR /usr/src/app

COPY requirements.txt ./

COPY . .

RUN pip3 install --no-cache-dir -r requirements.txt && \
    chmod 755 /usr/src/app/main.py