from python:3.6.4-slim-jessie

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

COPY . /usr/src/app

RUN apt-get update
RUN apt-get -y install gcc

RUN pip install pandas
RUN pip install CherryPy
RUN pip install lru-dict

EXPOSE 8080
ENTRYPOINT ["python", "ws.py"]
