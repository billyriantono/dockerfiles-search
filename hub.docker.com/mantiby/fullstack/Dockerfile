# Use an official Python runtime as a parent image
FROM python:3.7-slim

# Set environment varibles
ENV PYTHONUNBUFFERED 1
ENV DJANGO_SETTINGS_MODULE core.settings.dev

# Add directories
RUN mkdir -p /srv/fullstack/src/ && \
    mkdir -p /srv/fullstack/static/ && \
    mkdir -p /var/log/fullstack/

# Install any needed packages specified in requirements
COPY app/requirements.txt /tmp/requirements.txt
RUN pip install --trusted-host pypi.org --no-cache-dir --upgrade pip && \
    pip install --trusted-host pypi.org --no-cache-dir -r /tmp/requirements.txt

# Run gunicorn
EXPOSE 8765
WORKDIR /srv/fullstack/src/app/
CMD exec gunicorn core.wsgi:application --bind 0.0.0.0:8765 --workers 2
