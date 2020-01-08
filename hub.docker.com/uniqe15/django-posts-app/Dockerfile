FROM python:3.6
ENV PYTHONBUFFERED 1
ENV DJANGO_SETTINGS_MODULE "post_app.production_settings"
ENV ALLOWED_HOSTS "*"

RUN apt-get update && apt-get install -y netcat-openbsd

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

EXPOSE 8000
ENTRYPOINT bash -c "./scripts/setup.sh && ./scripts/run_server.sh"

