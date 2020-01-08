FROM python:3.7-slim

RUN set -ex && mkdir /var/app

WORKDIR /var/app

COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000

CMD python app.py