FROM python:2.7

WORKDIR /StreamClient

ENV PATH "$PATH:/StreamClient"


COPY client.py /StreamClient
COPY datastream_pb2_grpc.py /StreamClient
COPY datastream_pb2.py /StreamClient


RUN python -m pip install grpcio
RUN python -m pip install grpcio-tools googleapis-common-protos

CMD ["sh", "-c", "python ./client.py ${server}"]