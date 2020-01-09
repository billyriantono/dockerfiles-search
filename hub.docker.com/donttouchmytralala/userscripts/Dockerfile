FROM python:3

WORKDIR /usr/src/app


COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
RUN apt update
RUN apt install --no-install-recommends  mysql-client -y


COPY scripts/ /usr/src/app
