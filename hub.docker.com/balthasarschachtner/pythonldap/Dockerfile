FROM python:3
ENV PYTHONUNBUFFERED 1

RUN apt-get update && apt-get install -y libldap2-dev libsasl2-dev

RUN pip install ldap3
