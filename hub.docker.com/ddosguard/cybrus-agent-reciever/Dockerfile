FROM python:3-alpine

RUN set -x \
    && pip install --no-cache-dir \
       gunicorn \
       flask \
       redis

WORKDIR /app
CMD ["gunicorn", "-w", "4", "main:app"]

# vim: sw=4 sts=4 sr et
