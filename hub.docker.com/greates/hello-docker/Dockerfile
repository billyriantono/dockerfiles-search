FROM python:latest

RUN mkdir /app
WORKDIR /app
ADD index.html /app

CMD bash -c "cd /app; python3 -mhttp.server"

EXPOSE 8000


