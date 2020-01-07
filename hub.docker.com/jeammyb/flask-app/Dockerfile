FROM python:3.7.0-alpine

COPY . /app/flask-app
WORKDIR /app/flask-app

RUN pip install pipenv &&\
    pipenv install Flask    


CMD ["pipenv","run","python","app.py"]
