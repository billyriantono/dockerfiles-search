FROM python:3.6.8-stretch

WORKDIR /app
ENV AIRFLOW_HOME=/app
ENV SLUGIFY_USES_TEXT_UNIDECODE yes
ENV PYTHONPATH="$PYTHONPATH:/app/src"

ONBUILD COPY config/airflow.cfg /app/airflow.cfg

ONBUILD COPY requirements.txt /app
ONBUILD RUN pip install --no-cache-dir -r requirements.txt

ONBUILD COPY src src
