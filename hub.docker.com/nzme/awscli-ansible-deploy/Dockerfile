FROM python:2.7

MAINTAINER NZME <sysadmin@grabone.co.nz>

COPY ./requirements.txt /files/requirements.txt
WORKDIR /files/
RUN pip install -r requirements.txt && rm -rf /root/.cache/
