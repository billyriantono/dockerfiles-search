FROM python:3
ENV PYTHONBUFFERED 1
RUN mkdir /code
WORKDIR /code
COPY requirements.txt /code/
RUN apt-get update && apt-get install libsasl2-dev python-dev libldap2-dev libssl-dev -y && apt-get clean
RUN pip install -r requirements.txt
COPY manage.py quiz weasel LICENSE.md /code/
