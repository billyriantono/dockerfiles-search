FROM python:3.7-slim-stretch
WORKDIR /base
COPY requirements.txt /base
COPY CivisJobRunner.py /base
RUN pip install --trusted-host pypi.python.org -r requirements.txt
