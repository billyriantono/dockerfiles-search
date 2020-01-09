FROM python:alpine 

ENV MONGO_DATABASE=super-test
ENV MONGO_USER=mongoadmin
ENV MONGO_PASSWORD=secret
ENV MONGO_HOST=mongo-dev:27017

WORKDIR /src

ADD Pipfile /src/Pipfile
ADD app.py /src/app.py
ADD api /src/api

RUN pip install pipenv \
    && pipenv install

CMD pipenv run python /src/app.py 



