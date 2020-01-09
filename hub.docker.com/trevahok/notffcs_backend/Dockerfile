FROM python:3.6

MAINTAINER S.Vignesh (vighneshss@gmail.com)

COPY ./requirements.txt /app/requirements.txt

WORKDIR /app

RUN pip3 install -r requirements.txt

COPY . /app

EXPOSE 8000

CMD ["gunicorn","-w", "3", "-b", "0.0.0.0:8000", "app:app"]
