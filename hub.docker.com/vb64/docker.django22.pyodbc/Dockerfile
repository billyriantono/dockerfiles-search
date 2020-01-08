FROM python:3.7.2
MAINTAINER Vitaly Bogomolov <vit.sar68@gmail.com>

# Prepare the image.
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y -qq --no-install-recommends wget build-essential zlib1g-dev libjpeg-dev unzip python3-venv python3-dev openssh-client python-openssl gettext libcurl4-gnutls-dev libexpat1-dev libz-dev libssl-dev git unixodbc-dev && apt-get clean
RUN pip install --upgrade pip
RUN pip install coverage flake8 pylint Babel tester_coverage requests mock pyodbc "Django==2.2" django_tables2 pytz pylint-django gunicorn

CMD ["/bin/bash"]
