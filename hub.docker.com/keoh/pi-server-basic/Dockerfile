FROM python:3.7-alpine

ENV PYTHONUNBUFFERED 1
ENV INSTANCE 1

RUN mkdir /app

WORKDIR /app

ADD Pipfile /app/
ADD Pipfile.lock /app/

RUN pip install pipenv && pipenv install

ADD . /app/

EXPOSE 8080

CMD ["pipenv", "run", "python", "src/main.py"]