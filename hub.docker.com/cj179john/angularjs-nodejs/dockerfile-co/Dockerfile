FROM arm32v7/python:3-alpine

COPY ./pigpio.py ./

COPY ./ir-srv.conf ./
COPY ./ir-srv.py ./

CMD python3 ./ir-srv.py