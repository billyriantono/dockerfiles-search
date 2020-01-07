#
# Dockerfile for python2
#

FROM python:3-alpine

COPY pip.conf /etc/pip.conf

RUN pip3 install --no-cache-dir pipenv

CMD ["python", "--version"]
