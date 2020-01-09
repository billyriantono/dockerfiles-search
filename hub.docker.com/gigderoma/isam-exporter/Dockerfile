FROM python:2-slim

RUN mkdir -p /app/isam_exporter

WORKDIR /app/isam_exporter

COPY requirements.txt /app/isam_exporter
RUN pip install --no-cache-dir -r requirements.txt

COPY isam_exporter.py /app/isam_exporter

EXPOSE 8000

ENTRYPOINT [ "python", "-u", "./isam_exporter.py"]
