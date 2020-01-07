FROM python:3.7-slim

RUN apt-get update && apt-get install -y --no-install-recommends libmediainfo-dev && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip gunicorn

CMD ["python3"]
