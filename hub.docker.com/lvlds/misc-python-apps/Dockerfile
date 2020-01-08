FROM python:3.5

RUN mkdir -p /app/log
ADD . /app
WORKDIR /app
RUN pip install -r requirements.txt

EXPOSE 8080

ENTRYPOINT ["/app/docker-entrypoint.sh"]