FROM ubuntu
RUN apt-get update
RUN apt-get install -y net-tools python-pip python
COPY . /app
WORKDIR /app
CMD python myapp.py
