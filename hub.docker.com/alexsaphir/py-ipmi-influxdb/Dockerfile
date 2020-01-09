FROM python:3.7.2-stretch

WORKDIR /app

COPY . /app

RUN apt-get update
RUN apt-get install freeipmi-tools -y

RUN pip3 install numpy
RUN pip3 install influxdb

CMD ["python3", "app.py"]
