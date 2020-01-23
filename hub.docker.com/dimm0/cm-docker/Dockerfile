FROM python:2.7.13-slim

RUN apt-get update && apt-get install -y build-essential python-dev libffi-dev libssl-dev  && apt-get clean

RUN pip install cloudmesh.comet

ENTRYPOINT bash
