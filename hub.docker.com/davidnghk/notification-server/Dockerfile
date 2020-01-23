FROM tiangolo/uwsgi-nginx-flask:python3.6

ENV FLASK_PORT 80

COPY ./notification_server /app
COPY ./Pipfile /tmp
COPY ./Pipfile.lock /tmp

RUN pip3 install pipenv
RUN cd /tmp && pipenv install --system