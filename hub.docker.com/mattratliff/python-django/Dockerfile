FROM python:3.6-alpine3.7

RUN apk add --no-cache bash postgresql postgresql-client postgresql-dev gcc python3-dev musl-dev libressl-dev libffi-dev git xmlsec-dev

ENV PYTHONUNBUFFERED 1
ENV PROJECT_HOME=/code

RUN mkdir $PROJECT_HOME
WORKDIR $PROJECT_HOME

COPY ./requirements.txt $PROJECT_HOME
RUN pip install -r requirements.txt

COPY . $PROJECT_HOME

EXPOSE 8000

ADD ./docker-entrypoint.sh /
RUN chmod 755 /docker-entrypoint.sh
CMD ["/docker-entrypoint.sh"]