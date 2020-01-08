FROM python:3.7-alpine

WORKDIR /app

COPY main.py Pipfile Pipfile.lock ./

RUN pip install pipenv
RUN pipenv install

ENTRYPOINT ["pipenv", "run", "python", "main.py"]