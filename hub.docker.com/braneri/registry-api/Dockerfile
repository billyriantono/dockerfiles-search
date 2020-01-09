FROM python:3.7

COPY Pipfile /Pipfile

RUN pip install pipenv \
 && pipenv install --system --skip-lock

COPY src /src

EXPOSE 5000

ENTRYPOINT [ "python", "src/__main__.py" ]