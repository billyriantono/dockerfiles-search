FROM python:3.6

COPY . /app
WORKDIR /app

RUN apt-get update \
&& apt-get install -y git libpoppler-private-dev libpoppler-cpp-dev \
&& pip3 install cython \
&& pip3 install -r requirements.txt 

CMD ["gunicorn", "--workers=4","--timeout=3600", "-b 0.0.0.0:5000","wsgi:app"]

EXPOSE 5000
