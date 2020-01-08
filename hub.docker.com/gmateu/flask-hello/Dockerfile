FROM python:3

RUN pip install flask

RUN mkdir app/

COPY app.py /app/

WORKDIR /app

CMD FLASK_APP=app.py flask run --host=0.0.0.0
