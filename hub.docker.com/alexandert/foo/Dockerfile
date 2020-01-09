FROM python:3.6

WORKDIR /root

RUN mkdir -p www/hello-world

WORKDIR www/hello-world

COPY requirements.txt requirements.txt

RUN pip install -r requirements.txt

COPY . .

CMD ["./docker-entrypoint.sh"]
