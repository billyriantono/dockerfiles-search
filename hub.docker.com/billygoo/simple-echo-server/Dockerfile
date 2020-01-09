FROM      python:2.7-alpine

COPY      request_echo_server.py /myapp/
WORKDIR   /myapp

EXPOSE    8080

ENTRYPOINT ["python", "/myapp/request_echo_server.py"]
