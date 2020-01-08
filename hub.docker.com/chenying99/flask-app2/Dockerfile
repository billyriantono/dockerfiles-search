# FROM python:alpine
FROM python:3-alpine

RUN apk add --no-cache \
    build-base \
    && pip install gevent==1.4.0 \
    && apk del build-base

LABEL maintainer="Jeeva S. Chelladhurai"

COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
EXPOSE 5000
# ENTRYPOINT ["python", "run.py"]
CMD ["gunicorn", "-c", "gunicorn_config.py", "run:app"]

