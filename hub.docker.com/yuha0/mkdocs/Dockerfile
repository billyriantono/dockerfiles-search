FROM python:2.7-slim

RUN pip install mkdocs mkdocs-bootswatch
WORKDIR /mkdocs
VOLUME /mkdocs
EXPOSE 80

CMD mkdocs serve --dev-addr=0.0.0.0:80
