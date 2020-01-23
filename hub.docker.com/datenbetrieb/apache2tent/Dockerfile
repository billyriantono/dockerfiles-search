FROM python:3.7

LABEL maintainer="Data Machines Corp.<help@datamachines.io>"
LABEL grpc_version="1.15.0"
LABEL proto_version="3.6.1"
LABEL language="python:3.7"

ENV GRPC_PYTHON_VERSION 1.15.0
ENV PROTOBUF_PYTHON_VERSION 3.6.1

RUN python -m pip install --upgrade pip && \
    pip install tox autopep8 pytest protobuf==${PROTOBUF_PYTHON_VERSION} grpcio==${GRPC_PYTHON_VERSION} grpcio-tools==${GRPC_PYTHON_VERSION} grpcio-reflection==${GRPC_PYTHON_VERSION} grpcio-health-checking==${GRPC_PYTHON_VERSION} grpcio-testing==${GRPC_PYTHON_VERSION}
