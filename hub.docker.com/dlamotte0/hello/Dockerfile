FROM python:2.7-alpine
MAINTAINER Dan LaMotte "lamotte85@gmail.com"

RUN pip install Flask

WORKDIR /app
COPY app.py /app

CMD ["/usr/local/bin/python", "app.py"]
