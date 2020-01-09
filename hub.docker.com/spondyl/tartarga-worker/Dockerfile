FROM python:3.6-alpine

RUN mkdir /code
WORKDIR /code
RUN apk add --update --no-cache gcc libc-dev libxslt-dev
COPY requirements.txt /code
RUN pip install -r requirements.txt
COPY . /code/

CMD celery -A tasks worker --beat --loglevel=info