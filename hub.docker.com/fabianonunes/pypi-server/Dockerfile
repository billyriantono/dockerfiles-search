FROM python:2.7-slim-stretch

RUN pip install pipenv

RUN adduser --system --uid 1000 --group --home /app runner;
USER runner
WORKDIR /app

COPY Pipfile* /app/
RUN pipenv install --deploy

ENTRYPOINT [ "pipenv", "run" ]
CMD [ "pypi-server", "--port", "7777", "/packages" ]
