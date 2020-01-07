FROM python:latest
MAINTAINER jpacg <jpacg0@gmail.com>

# Install uWSGI
RUN pip --no-cache-dir install uwsgi

# Install Requirements
COPY requirements.txt /requirements.txt
RUN pip --no-cache-dir install -r /requirements.txt

# Copy the base uWSGI ini file to enable default dynamic uwsgi process number
COPY uwsgi.ini /etc/uwsgi/

COPY ./app /app
WORKDIR /app

CMD ["/usr/local/bin/uwsgi", "--ini", "/etc/uwsgi/uwsgi.ini", "--ini", "/app/uwsgi.ini"]