FROM python:3.7

MAINTAINER Tomasz Chalupnik <tchalupnik@gmail.com>

RUN apt-get update && \
    apt-get install -y postgresql-client libpq-dev && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /var/app
WORKDIR /var/app

ENV PYTHONUNBUFFERED 1
COPY app /var/app/.
RUN pip install -r requirements.txt
CMD chmod +x /var/app/runserver.sh

EXPOSE 8000

CMD ["/var/app/runserver.sh"]
