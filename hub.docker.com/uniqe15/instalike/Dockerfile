FROM python:3.6

ENV PYTHONUNBUFFERED 1
ENV DB_TYPE 'docker'

RUN apt-get update
RUN apt-get install netcat --assume-yes

RUN git clone https://gitlab.com/kamilgregorczyk/instalike.git
WORKDIR instalike

RUN pip install -r requirements.txt
RUN python manage.py collectstatic --no-input
