FROM squidfunk/mkdocs-material:4.6.0 AS builder

ADD mkdocs /docs

WORKDIR /docs
RUN pip install --upgrade pip==19.3.1 && \
    pip install pipenv==2018.11.26 && \
    pipenv install && \
    pipenv run mkdocs build

FROM nginx:1.17.6-alpine
LABEL maintainer="Ed Meagher <ed@meagherfamily.org>"

COPY --from=builder /docs/site /usr/share/nginx/html

EXPOSE 80
