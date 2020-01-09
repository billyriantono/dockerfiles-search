FROM python:3.7.1-alpine3.8

ARG PORT=8080

ENV PORT ${PORT}

RUN pip install mkdocs \
                click-man \
                pymdown-extensions \
                mkdocs-material

WORKDIR /mkdocs

EXPOSE ${PORT}

CMD mkdocs serve
