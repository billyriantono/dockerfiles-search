FROM python:2.7
MAINTAINER Thuan Duong "thuandt26@gmail.com"
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENTRYPOINT ["gunicorn"]
CMD ["--bind", "0.0.0.0:5000", "wsgi:app"]
