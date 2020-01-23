FROM python:3.6-slim
ENV PYTHONUNBUFFERED 1
RUN mkdir /hotcredits
WORKDIR /hotcredits
COPY requirements.txt /hotcredits/
RUN pip install -r requirements.txt
COPY . /hotcredits/
