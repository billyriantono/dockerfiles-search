FROM python:3.7-alpine

WORKDIR /app

ENV PIP_NO_CACHE_DIR false
RUN pip install pipenv
COPY Pipfile /app
COPY Pipfile.lock /app
RUN pipenv install --deploy --system

COPY . /app

EXPOSE 8000

CMD ["gunicorn", "-b", ":8000", "--capture-output", "app:main()"]
