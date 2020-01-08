FROM ubuntu:latest

RUN apt-get update && apt-get install -y python python-pip
RUN pip install flask

COPY hello.py /tmp/hello.py

EXPOSE 5000

CMD ["python", "/tmp/hello.py"]

